---
title: Azure API Management-paginabesturingselementen | Microsoft Docs
description: Meer informatie over de paginabesturingselementen beschikbaar voor gebruik in developer portal sjablonen in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1ce0657aebe34d093ae94281de208c929067742a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="34fd9-103">Azure API Management-paginabesturingselementen</span><span class="sxs-lookup"><span data-stu-id="34fd9-103">Azure API Management page controls</span></span>
<span data-ttu-id="34fd9-104">Azure API Management biedt de volgende besturingselementen voor gebruik in het developer portal sjablonen.</span><span class="sxs-lookup"><span data-stu-id="34fd9-104">Azure API Management provides the following controls for use in the developer portal templates.</span></span>  
  
 <span data-ttu-id="34fd9-105">Plaats deze in de gewenste locatie in de portal developer-sjabloon voor het gebruik van een besturingselement.</span><span class="sxs-lookup"><span data-stu-id="34fd9-105">To use a control, place it in the desired location in the developer portal template.</span></span> <span data-ttu-id="34fd9-106">Sommige besturingselementen, zoals de [acties voor app](#app-actions) bepalen, parameters hebben, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="34fd9-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="34fd9-107">De waarden voor de parameters worden doorgegeven als onderdeel van het gegevensmodel voor de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="34fd9-107">The values for the parameters are passed in as part of the data model for the template.</span></span> <span data-ttu-id="34fd9-108">In de meeste gevallen kunt u gewoon plakken in het opgegeven voorbeeld voor elk besturingselement om correct te laten werken.</span><span class="sxs-lookup"><span data-stu-id="34fd9-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span></span> <span data-ttu-id="34fd9-109">Voor meer informatie over de parameterwaarden ziet u de sectie voor het model van gegevens voor elke sjabloon waarin een besturingselement kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="34fd9-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="34fd9-110">Zie voor meer informatie over het werken met sjablonen [het aanpassen van de API Management portal voor ontwikkelaars met behulp van sjablonen](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="34fd9-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="34fd9-111">Paginabesturingselementen voor ontwikkelaars sjabloon</span><span class="sxs-lookup"><span data-stu-id="34fd9-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="34fd9-112">App-acties</span><span class="sxs-lookup"><span data-stu-id="34fd9-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="34fd9-113">Basic-aanmelding</span><span class="sxs-lookup"><span data-stu-id="34fd9-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="34fd9-114">besturingselement voor paginering</span><span class="sxs-lookup"><span data-stu-id="34fd9-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="34fd9-115">providers</span><span class="sxs-lookup"><span data-stu-id="34fd9-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="34fd9-116">besturingselement voor zoeken</span><span class="sxs-lookup"><span data-stu-id="34fd9-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="34fd9-117">aanmelden</span><span class="sxs-lookup"><span data-stu-id="34fd9-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="34fd9-118">abonneren knop</span><span class="sxs-lookup"><span data-stu-id="34fd9-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="34fd9-119">abonnement annuleren</span><span class="sxs-lookup"><span data-stu-id="34fd9-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="34fd9-120"><a name="app-actions"></a>App-acties</span><span class="sxs-lookup"><span data-stu-id="34fd9-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="34fd9-121">De `app-actions` beheer biedt een gebruikersinterface voor interactie met toepassingen op de pagina gebruikersprofiel in de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="34fd9-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="34fd9-122">![App- &#45; acties besturingselement](./media/api-management-page-controls/APIM-app-actions-control.png "APIM acties voor app beheer")</span><span class="sxs-lookup"><span data-stu-id="34fd9-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="34fd9-123">Gebruik</span><span class="sxs-lookup"><span data-stu-id="34fd9-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="34fd9-124">Parameters</span><span class="sxs-lookup"><span data-stu-id="34fd9-124">Parameters</span></span>  
  
|<span data-ttu-id="34fd9-125">Parameter</span><span class="sxs-lookup"><span data-stu-id="34fd9-125">Parameter</span></span>|<span data-ttu-id="34fd9-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34fd9-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="34fd9-127">AppId</span><span class="sxs-lookup"><span data-stu-id="34fd9-127">appId</span></span>|<span data-ttu-id="34fd9-128">De id van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="34fd9-128">The id of the application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="34fd9-129">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="34fd9-129">Developer portal templates</span></span>  
 <span data-ttu-id="34fd9-130">De `app-actions` besturingselement kan worden gebruikt in de volgende sjablonen van de developer-portal.</span><span class="sxs-lookup"><span data-stu-id="34fd9-130">The `app-actions` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="34fd9-131">Toepassingen</span><span class="sxs-lookup"><span data-stu-id="34fd9-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="34fd9-132"><a name="basic-signin"></a>Basic-aanmelding</span><span class="sxs-lookup"><span data-stu-id="34fd9-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="34fd9-133">De `basic-signin` control biedt een besturingselement voor het verzamelen van de gebruiker aanmelden informatie in de aanmeldingspagina in de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="34fd9-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="34fd9-134">![Basic &#45; signin-besturingselement](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic signin-besturingselement")</span><span class="sxs-lookup"><span data-stu-id="34fd9-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="34fd9-135">Gebruik</span><span class="sxs-lookup"><span data-stu-id="34fd9-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="34fd9-136">Parameters</span><span class="sxs-lookup"><span data-stu-id="34fd9-136">Parameters</span></span>  
 <span data-ttu-id="34fd9-137">Geen.</span><span class="sxs-lookup"><span data-stu-id="34fd9-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="34fd9-138">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="34fd9-138">Developer portal templates</span></span>  
 <span data-ttu-id="34fd9-139">De `basic-signin` besturingselement kan worden gebruikt in de volgende sjablonen van de developer-portal.</span><span class="sxs-lookup"><span data-stu-id="34fd9-139">The `basic-signin` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="34fd9-140">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="34fd9-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="34fd9-141"><a name="paging-control"></a>besturingselement voor paginering</span><span class="sxs-lookup"><span data-stu-id="34fd9-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="34fd9-142">De `paging-control` biedt pagineringsfunctionaliteit moet worden ingeschakeld op developer portal-pagina's die een lijst met items weergeven.</span><span class="sxs-lookup"><span data-stu-id="34fd9-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="34fd9-143">![besturingselement van het wisselbestand](./media/api-management-page-controls/APIM-paging-control.png "APIM paginering besturingselement")</span><span class="sxs-lookup"><span data-stu-id="34fd9-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="34fd9-144">Gebruik</span><span class="sxs-lookup"><span data-stu-id="34fd9-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="34fd9-145">Parameters</span><span class="sxs-lookup"><span data-stu-id="34fd9-145">Parameters</span></span>  
 <span data-ttu-id="34fd9-146">Geen.</span><span class="sxs-lookup"><span data-stu-id="34fd9-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="34fd9-147">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="34fd9-147">Developer portal templates</span></span>  
 <span data-ttu-id="34fd9-148">De `paging-control` besturingselement kan worden gebruikt in de volgende sjablonen van de developer-portal.</span><span class="sxs-lookup"><span data-stu-id="34fd9-148">The `paging-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="34fd9-149">API-lijst</span><span class="sxs-lookup"><span data-stu-id="34fd9-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="34fd9-150">Lijst met kwesties</span><span class="sxs-lookup"><span data-stu-id="34fd9-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="34fd9-151">Lijst met producten</span><span class="sxs-lookup"><span data-stu-id="34fd9-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="34fd9-152"><a name="providers"></a>providers</span><span class="sxs-lookup"><span data-stu-id="34fd9-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="34fd9-153">De `providers` beheer biedt een controle voor selectie van verificatieproviders in de aanmeldingspagina in de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="34fd9-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="34fd9-154">![providers besturingselement](./media/api-management-page-controls/APIM-providers-control.png "APIM providers besturingselement")</span><span class="sxs-lookup"><span data-stu-id="34fd9-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="34fd9-155">Gebruik</span><span class="sxs-lookup"><span data-stu-id="34fd9-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="34fd9-156">Parameters</span><span class="sxs-lookup"><span data-stu-id="34fd9-156">Parameters</span></span>  
 <span data-ttu-id="34fd9-157">Geen.</span><span class="sxs-lookup"><span data-stu-id="34fd9-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="34fd9-158">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="34fd9-158">Developer portal templates</span></span>  
 <span data-ttu-id="34fd9-159">De `providers` besturingselement kan worden gebruikt in de volgende sjablonen van de developer-portal.</span><span class="sxs-lookup"><span data-stu-id="34fd9-159">The `providers` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="34fd9-160">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="34fd9-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="34fd9-161"><a name="search-control"></a>besturingselement voor zoeken</span><span class="sxs-lookup"><span data-stu-id="34fd9-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="34fd9-162">De `search-control` biedt functionaliteit voor het zoeken op developer portal-pagina's die een lijst met items weergeven.</span><span class="sxs-lookup"><span data-stu-id="34fd9-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="34fd9-163">![besturingselement zoeken](./media/api-management-page-controls/APIM-search-control.png "APIM zoekbesturing")</span><span class="sxs-lookup"><span data-stu-id="34fd9-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="34fd9-164">Gebruik</span><span class="sxs-lookup"><span data-stu-id="34fd9-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="34fd9-165">Parameters</span><span class="sxs-lookup"><span data-stu-id="34fd9-165">Parameters</span></span>  
 <span data-ttu-id="34fd9-166">Geen.</span><span class="sxs-lookup"><span data-stu-id="34fd9-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="34fd9-167">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="34fd9-167">Developer portal templates</span></span>  
 <span data-ttu-id="34fd9-168">De `search-control` besturingselement kan worden gebruikt in de volgende sjablonen van de developer-portal.</span><span class="sxs-lookup"><span data-stu-id="34fd9-168">The `search-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="34fd9-169">API-lijst</span><span class="sxs-lookup"><span data-stu-id="34fd9-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="34fd9-170">Lijst met producten</span><span class="sxs-lookup"><span data-stu-id="34fd9-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="34fd9-171"><a name="sign-up"></a>aanmelden</span><span class="sxs-lookup"><span data-stu-id="34fd9-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="34fd9-172">De `sign-up` control biedt een besturingselement voor het verzamelen van informatie over gebruikersprofielen in de registratiepagina in de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="34fd9-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="34fd9-173">![aanmelding &#45; besturingselement up](./media/api-management-page-controls/APIM-sign-up-control.png "APIM aanmelding besturingselement")</span><span class="sxs-lookup"><span data-stu-id="34fd9-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="34fd9-174">Gebruik</span><span class="sxs-lookup"><span data-stu-id="34fd9-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="34fd9-175">Parameters</span><span class="sxs-lookup"><span data-stu-id="34fd9-175">Parameters</span></span>  
 <span data-ttu-id="34fd9-176">Geen.</span><span class="sxs-lookup"><span data-stu-id="34fd9-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="34fd9-177">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="34fd9-177">Developer portal templates</span></span>  
 <span data-ttu-id="34fd9-178">De `sign-up` besturingselement kan worden gebruikt in de volgende sjablonen van de developer-portal.</span><span class="sxs-lookup"><span data-stu-id="34fd9-178">The `sign-up` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="34fd9-179">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="34fd9-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="34fd9-180"><a name="subscribe-button"></a>abonneren knop</span><span class="sxs-lookup"><span data-stu-id="34fd9-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="34fd9-181">De `subscribe-button` biedt een controle voor een gebruiker op een product abonneren.</span><span class="sxs-lookup"><span data-stu-id="34fd9-181">The `subscribe-button` provides a control for subscribing a user to a product.</span></span>  
  
 <span data-ttu-id="34fd9-182">![abonneren &#45; knopbesturingselement](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM abonneren knopbesturingselement")</span><span class="sxs-lookup"><span data-stu-id="34fd9-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="34fd9-183">Gebruik</span><span class="sxs-lookup"><span data-stu-id="34fd9-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="34fd9-184">Parameters</span><span class="sxs-lookup"><span data-stu-id="34fd9-184">Parameters</span></span>  
 <span data-ttu-id="34fd9-185">Geen.</span><span class="sxs-lookup"><span data-stu-id="34fd9-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="34fd9-186">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="34fd9-186">Developer portal templates</span></span>  
 <span data-ttu-id="34fd9-187">De `subscribe-button` besturingselement kan worden gebruikt in de volgende sjablonen van de developer-portal.</span><span class="sxs-lookup"><span data-stu-id="34fd9-187">The `subscribe-button` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="34fd9-188">Product</span><span class="sxs-lookup"><span data-stu-id="34fd9-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="34fd9-189"><a name="subscription-cancel"></a>abonnement annuleren</span><span class="sxs-lookup"><span data-stu-id="34fd9-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="34fd9-190">De `subscription-cancel` control biedt een besturingselement voor het annuleren van een abonnement op een product in de pagina gebruikersprofiel in de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="34fd9-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="34fd9-191">![abonnement &#45; besturing annuleren](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM abonnement annuleren besturingselement")</span><span class="sxs-lookup"><span data-stu-id="34fd9-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="34fd9-192">Gebruik</span><span class="sxs-lookup"><span data-stu-id="34fd9-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="34fd9-193">Parameters</span><span class="sxs-lookup"><span data-stu-id="34fd9-193">Parameters</span></span>  
  
|<span data-ttu-id="34fd9-194">Parameter</span><span class="sxs-lookup"><span data-stu-id="34fd9-194">Parameter</span></span>|<span data-ttu-id="34fd9-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="34fd9-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="34fd9-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="34fd9-196">subscriptionId</span></span>|<span data-ttu-id="34fd9-197">De id van het abonnement te annuleren.</span><span class="sxs-lookup"><span data-stu-id="34fd9-197">The id of the subscription to cancel.</span></span>|  
|<span data-ttu-id="34fd9-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="34fd9-198">cancelUrl</span></span>|<span data-ttu-id="34fd9-199">De URL van abonnement annuleren.</span><span class="sxs-lookup"><span data-stu-id="34fd9-199">The subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="34fd9-200">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="34fd9-200">Developer portal templates</span></span>  
 <span data-ttu-id="34fd9-201">De `subscription-cancel` besturingselement kan worden gebruikt in de volgende sjablonen van de developer-portal.</span><span class="sxs-lookup"><span data-stu-id="34fd9-201">The `subscription-cancel` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="34fd9-202">Product</span><span class="sxs-lookup"><span data-stu-id="34fd9-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="34fd9-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34fd9-203">Next steps</span></span>
<span data-ttu-id="34fd9-204">Zie voor meer informatie over het werken met sjablonen [het aanpassen van de API Management portal voor ontwikkelaars met behulp van sjablonen](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="34fd9-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
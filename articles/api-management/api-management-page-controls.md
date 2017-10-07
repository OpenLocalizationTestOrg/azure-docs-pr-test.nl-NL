---
title: aaaAzure API Management paginabesturingselementen | Microsoft Docs
description: Meer informatie over Hallo paginabesturingselementen beschikbaar voor gebruik in developer portal sjablonen in Azure API Management.
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
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="a95d9-103">Azure API Management-paginabesturingselementen</span><span class="sxs-lookup"><span data-stu-id="a95d9-103">Azure API Management page controls</span></span>
<span data-ttu-id="a95d9-104">Azure API Management biedt Hallo besturingselementen voor gebruik in Hallo developer portal sjablonen te volgen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-104">Azure API Management provides hello following controls for use in hello developer portal templates.</span></span>  
  
 <span data-ttu-id="a95d9-105">toouse een besturingselement op Hallo gewenste locatie plaatst in Hallo developer portal sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a95d9-105">toouse a control, place it in hello desired location in hello developer portal template.</span></span> <span data-ttu-id="a95d9-106">Sommige besturingselementen, zoals Hallo [acties voor app](#app-actions) bepalen, parameters hebben, zoals wordt weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-106">Some controls, such as hello [app-actions](#app-actions) control, have parameters, as shown in hello following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="a95d9-107">Hallo-waarden voor Hallo parameters worden doorgegeven in als onderdeel van het gegevensmodel Hallo voor Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a95d9-107">hello values for hello parameters are passed in as part of hello data model for hello template.</span></span> <span data-ttu-id="a95d9-108">In de meeste gevallen kunt u gewoon plakken Hallo opgegeven voorbeeld voor elk besturingselement voor het toowork correct.</span><span class="sxs-lookup"><span data-stu-id="a95d9-108">In most cases, you can simply paste in hello provided example for each control for it toowork correctly.</span></span> <span data-ttu-id="a95d9-109">U ziet voor meer informatie over de parameterwaarden Hallo Hallo gegevenssectie model voor elke sjabloon waarin een besturingselement kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a95d9-109">For more information on hello parameter values, you can see hello data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="a95d9-110">Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="a95d9-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="a95d9-111">Paginabesturingselementen voor ontwikkelaars sjabloon</span><span class="sxs-lookup"><span data-stu-id="a95d9-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="a95d9-112">App-acties</span><span class="sxs-lookup"><span data-stu-id="a95d9-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="a95d9-113">Basic-aanmelding</span><span class="sxs-lookup"><span data-stu-id="a95d9-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="a95d9-114">besturingselement voor paginering</span><span class="sxs-lookup"><span data-stu-id="a95d9-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="a95d9-115">providers</span><span class="sxs-lookup"><span data-stu-id="a95d9-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="a95d9-116">besturingselement voor zoeken</span><span class="sxs-lookup"><span data-stu-id="a95d9-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="a95d9-117">aanmelden</span><span class="sxs-lookup"><span data-stu-id="a95d9-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="a95d9-118">abonneren knop</span><span class="sxs-lookup"><span data-stu-id="a95d9-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="a95d9-119">abonnement annuleren</span><span class="sxs-lookup"><span data-stu-id="a95d9-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="a95d9-120"><a name="app-actions"></a>App-acties</span><span class="sxs-lookup"><span data-stu-id="a95d9-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="a95d9-121">Hallo `app-actions` beheer biedt een gebruikersinterface voor interactie met toepassingen op Hallo pagina gebruikersprofiel in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="a95d9-121">hello `app-actions` control provides a user interface for interacting with applications on hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="a95d9-122">![App- &#45; acties besturingselement](./media/api-management-page-controls/APIM-app-actions-control.png "APIM acties voor app beheer")</span><span class="sxs-lookup"><span data-stu-id="a95d9-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="a95d9-123">Gebruik</span><span class="sxs-lookup"><span data-stu-id="a95d9-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="a95d9-124">Parameters</span><span class="sxs-lookup"><span data-stu-id="a95d9-124">Parameters</span></span>  
  
|<span data-ttu-id="a95d9-125">Parameter</span><span class="sxs-lookup"><span data-stu-id="a95d9-125">Parameter</span></span>|<span data-ttu-id="a95d9-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a95d9-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="a95d9-127">AppId</span><span class="sxs-lookup"><span data-stu-id="a95d9-127">appId</span></span>|<span data-ttu-id="a95d9-128">Hallo-id van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="a95d9-128">hello id of hello application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="a95d9-129">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="a95d9-129">Developer portal templates</span></span>  
 <span data-ttu-id="a95d9-130">Hallo `app-actions` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-130">hello `app-actions` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="a95d9-131">Toepassingen</span><span class="sxs-lookup"><span data-stu-id="a95d9-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="a95d9-132"><a name="basic-signin"></a>Basic-aanmelding</span><span class="sxs-lookup"><span data-stu-id="a95d9-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="a95d9-133">Hallo `basic-signin` beheer biedt een controle voor verzamelen gebruiker aanmelden informatie in Hallo pagina in de ontwikkelaarsportal Hallo aanmelden.</span><span class="sxs-lookup"><span data-stu-id="a95d9-133">hello `basic-signin` control provides a control for collecting user sign in information in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="a95d9-134">![Basic &#45; signin-besturingselement](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic signin-besturingselement")</span><span class="sxs-lookup"><span data-stu-id="a95d9-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="a95d9-135">Gebruik</span><span class="sxs-lookup"><span data-stu-id="a95d9-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="a95d9-136">Parameters</span><span class="sxs-lookup"><span data-stu-id="a95d9-136">Parameters</span></span>  
 <span data-ttu-id="a95d9-137">Geen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="a95d9-138">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="a95d9-138">Developer portal templates</span></span>  
 <span data-ttu-id="a95d9-139">Hallo `basic-signin` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-139">hello `basic-signin` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="a95d9-140">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="a95d9-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="a95d9-141"><a name="paging-control"></a>besturingselement voor paginering</span><span class="sxs-lookup"><span data-stu-id="a95d9-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="a95d9-142">Hallo `paging-control` biedt pagineringsfunctionaliteit moet worden ingeschakeld op developer portal-pagina's die een lijst met items weergeven.</span><span class="sxs-lookup"><span data-stu-id="a95d9-142">hello `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="a95d9-143">![besturingselement van het wisselbestand](./media/api-management-page-controls/APIM-paging-control.png "APIM paginering besturingselement")</span><span class="sxs-lookup"><span data-stu-id="a95d9-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="a95d9-144">Gebruik</span><span class="sxs-lookup"><span data-stu-id="a95d9-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="a95d9-145">Parameters</span><span class="sxs-lookup"><span data-stu-id="a95d9-145">Parameters</span></span>  
 <span data-ttu-id="a95d9-146">Geen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="a95d9-147">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="a95d9-147">Developer portal templates</span></span>  
 <span data-ttu-id="a95d9-148">Hallo `paging-control` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-148">hello `paging-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="a95d9-149">API-lijst</span><span class="sxs-lookup"><span data-stu-id="a95d9-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="a95d9-150">Lijst met kwesties</span><span class="sxs-lookup"><span data-stu-id="a95d9-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="a95d9-151">Lijst met producten</span><span class="sxs-lookup"><span data-stu-id="a95d9-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="a95d9-152"><a name="providers"></a>providers</span><span class="sxs-lookup"><span data-stu-id="a95d9-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="a95d9-153">Hallo `providers` beheer biedt een controle voor selectie van verificatieproviders in Hallo aanmeldingspagina in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="a95d9-153">hello `providers` control provides a control for selection of authentication providers in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="a95d9-154">![providers besturingselement](./media/api-management-page-controls/APIM-providers-control.png "APIM providers besturingselement")</span><span class="sxs-lookup"><span data-stu-id="a95d9-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="a95d9-155">Gebruik</span><span class="sxs-lookup"><span data-stu-id="a95d9-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="a95d9-156">Parameters</span><span class="sxs-lookup"><span data-stu-id="a95d9-156">Parameters</span></span>  
 <span data-ttu-id="a95d9-157">Geen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="a95d9-158">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="a95d9-158">Developer portal templates</span></span>  
 <span data-ttu-id="a95d9-159">Hallo `providers` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-159">hello `providers` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="a95d9-160">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="a95d9-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="a95d9-161"><a name="search-control"></a>besturingselement voor zoeken</span><span class="sxs-lookup"><span data-stu-id="a95d9-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="a95d9-162">Hallo `search-control` biedt functionaliteit voor het zoeken op developer portal-pagina's die een lijst met items weergeven.</span><span class="sxs-lookup"><span data-stu-id="a95d9-162">hello `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="a95d9-163">![besturingselement zoeken](./media/api-management-page-controls/APIM-search-control.png "APIM zoekbesturing")</span><span class="sxs-lookup"><span data-stu-id="a95d9-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="a95d9-164">Gebruik</span><span class="sxs-lookup"><span data-stu-id="a95d9-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="a95d9-165">Parameters</span><span class="sxs-lookup"><span data-stu-id="a95d9-165">Parameters</span></span>  
 <span data-ttu-id="a95d9-166">Geen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="a95d9-167">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="a95d9-167">Developer portal templates</span></span>  
 <span data-ttu-id="a95d9-168">Hallo `search-control` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-168">hello `search-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="a95d9-169">API-lijst</span><span class="sxs-lookup"><span data-stu-id="a95d9-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="a95d9-170">Lijst met producten</span><span class="sxs-lookup"><span data-stu-id="a95d9-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="a95d9-171"><a name="sign-up"></a>aanmelden</span><span class="sxs-lookup"><span data-stu-id="a95d9-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="a95d9-172">Hallo `sign-up` control biedt een besturingselement voor het verzamelen van gebruikersprofielgegevens in Hallo registratiepagina in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="a95d9-172">hello `sign-up` control provides a control for collecting user profile information in hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="a95d9-173">![aanmelding &#45; besturingselement up](./media/api-management-page-controls/APIM-sign-up-control.png "APIM aanmelding besturingselement")</span><span class="sxs-lookup"><span data-stu-id="a95d9-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="a95d9-174">Gebruik</span><span class="sxs-lookup"><span data-stu-id="a95d9-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="a95d9-175">Parameters</span><span class="sxs-lookup"><span data-stu-id="a95d9-175">Parameters</span></span>  
 <span data-ttu-id="a95d9-176">Geen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="a95d9-177">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="a95d9-177">Developer portal templates</span></span>  
 <span data-ttu-id="a95d9-178">Hallo `sign-up` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-178">hello `sign-up` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="a95d9-179">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="a95d9-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="a95d9-180"><a name="subscribe-button"></a>abonneren knop</span><span class="sxs-lookup"><span data-stu-id="a95d9-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="a95d9-181">Hallo `subscribe-button` biedt een controle voor een gebruiker tooa product abonneren.</span><span class="sxs-lookup"><span data-stu-id="a95d9-181">hello `subscribe-button` provides a control for subscribing a user tooa product.</span></span>  
  
 <span data-ttu-id="a95d9-182">![abonneren &#45; knopbesturingselement](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM abonneren knopbesturingselement")</span><span class="sxs-lookup"><span data-stu-id="a95d9-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="a95d9-183">Gebruik</span><span class="sxs-lookup"><span data-stu-id="a95d9-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="a95d9-184">Parameters</span><span class="sxs-lookup"><span data-stu-id="a95d9-184">Parameters</span></span>  
 <span data-ttu-id="a95d9-185">Geen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="a95d9-186">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="a95d9-186">Developer portal templates</span></span>  
 <span data-ttu-id="a95d9-187">Hallo `subscribe-button` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-187">hello `subscribe-button` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="a95d9-188">Product</span><span class="sxs-lookup"><span data-stu-id="a95d9-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="a95d9-189"><a name="subscription-cancel"></a>abonnement annuleren</span><span class="sxs-lookup"><span data-stu-id="a95d9-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="a95d9-190">Hallo `subscription-cancel` control biedt een besturingselement voor het annuleren van een abonnement tooa product Hallo pagina gebruikersprofiel in Hallo-portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="a95d9-190">hello `subscription-cancel` control provides a control for cancelling a subscription tooa product in hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="a95d9-191">![abonnement &#45; besturing annuleren](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM abonnement annuleren besturingselement")</span><span class="sxs-lookup"><span data-stu-id="a95d9-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="a95d9-192">Gebruik</span><span class="sxs-lookup"><span data-stu-id="a95d9-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="a95d9-193">Parameters</span><span class="sxs-lookup"><span data-stu-id="a95d9-193">Parameters</span></span>  
  
|<span data-ttu-id="a95d9-194">Parameter</span><span class="sxs-lookup"><span data-stu-id="a95d9-194">Parameter</span></span>|<span data-ttu-id="a95d9-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a95d9-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="a95d9-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="a95d9-196">subscriptionId</span></span>|<span data-ttu-id="a95d9-197">Hallo-id van Hallo abonnement toocancel.</span><span class="sxs-lookup"><span data-stu-id="a95d9-197">hello id of hello subscription toocancel.</span></span>|  
|<span data-ttu-id="a95d9-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="a95d9-198">cancelUrl</span></span>|<span data-ttu-id="a95d9-199">Hallo abonnement annuleren URL.</span><span class="sxs-lookup"><span data-stu-id="a95d9-199">hello subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="a95d9-200">Developer portal-sjablonen</span><span class="sxs-lookup"><span data-stu-id="a95d9-200">Developer portal templates</span></span>  
 <span data-ttu-id="a95d9-201">Hallo `subscription-cancel` besturingselement kan worden gebruikt in Hallo developer portal-sjablonen te volgen.</span><span class="sxs-lookup"><span data-stu-id="a95d9-201">hello `subscription-cancel` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="a95d9-202">Product</span><span class="sxs-lookup"><span data-stu-id="a95d9-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="a95d9-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a95d9-203">Next steps</span></span>
<span data-ttu-id="a95d9-204">Zie voor meer informatie over het werken met sjablonen [hoe toocustomize API Management-portal voor ontwikkelaars met behulp van sjablonen Hallo](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a95d9-204">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>

---
title: verificatiebeleid voor aaaAzure API Management | Microsoft Docs
description: Meer informatie over Hallo verificatiebeleid beschikbaar voor gebruik in Azure API Management.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="a7c18-103">API Management-beleidsregels voor verificatie</span><span class="sxs-lookup"><span data-stu-id="a7c18-103">API Management authentication policies</span></span>
<span data-ttu-id="a7c18-104">Dit onderwerp bevat een verwijzing voor Hallo API Management-beleidsregels te volgen.</span><span class="sxs-lookup"><span data-stu-id="a7c18-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="a7c18-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="a7c18-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="a7c18-106"><a name="AuthenticationPolicies"></a>Verificatiebeleid</span><span class="sxs-lookup"><span data-stu-id="a7c18-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="a7c18-107">[Verificatie met Basic](api-management-authentication-policies.md#Basic) -verificatie met een back-endservice basisverificatie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a7c18-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="a7c18-108">[Verificatie met een clientcertificaat](api-management-authentication-policies.md#ClientCertificate) -verificatie met een back-endservice met behulp van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="a7c18-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="a7c18-109"><a name="Basic"></a>Verificatie met Basic</span><span class="sxs-lookup"><span data-stu-id="a7c18-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="a7c18-110">Gebruik Hallo `authentication-basic` beleid tooauthenticate met een back-endservice basisverificatie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a7c18-110">Use hello `authentication-basic` policy tooauthenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="a7c18-111">Dit beleid effectief Hallo HTTP-autorisatie-header toohello waarde bijbehorende toohello referenties instellen in het Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="a7c18-111">This policy effectively sets hello HTTP Authorization header toohello value corresponding toohello credentials provided in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="a7c18-112">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="a7c18-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="a7c18-113">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="a7c18-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="a7c18-114">Elementen</span><span class="sxs-lookup"><span data-stu-id="a7c18-114">Elements</span></span>  
  
|<span data-ttu-id="a7c18-115">Naam</span><span class="sxs-lookup"><span data-stu-id="a7c18-115">Name</span></span>|<span data-ttu-id="a7c18-116">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a7c18-116">Description</span></span>|<span data-ttu-id="a7c18-117">Vereist</span><span class="sxs-lookup"><span data-stu-id="a7c18-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="a7c18-118">verificatie-basis</span><span class="sxs-lookup"><span data-stu-id="a7c18-118">authentication-basic</span></span>|<span data-ttu-id="a7c18-119">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="a7c18-119">Root element.</span></span>|<span data-ttu-id="a7c18-120">Ja</span><span class="sxs-lookup"><span data-stu-id="a7c18-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="a7c18-121">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="a7c18-121">Attributes</span></span>  
  
|<span data-ttu-id="a7c18-122">Naam</span><span class="sxs-lookup"><span data-stu-id="a7c18-122">Name</span></span>|<span data-ttu-id="a7c18-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a7c18-123">Description</span></span>|<span data-ttu-id="a7c18-124">Vereist</span><span class="sxs-lookup"><span data-stu-id="a7c18-124">Required</span></span>|<span data-ttu-id="a7c18-125">Standaard</span><span class="sxs-lookup"><span data-stu-id="a7c18-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="a7c18-126">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="a7c18-126">username</span></span>|<span data-ttu-id="a7c18-127">Hiermee geeft u een gebruikersnaam Hallo Hallo Basic referentie.</span><span class="sxs-lookup"><span data-stu-id="a7c18-127">Specifies hello username of hello Basic credential.</span></span>|<span data-ttu-id="a7c18-128">Ja</span><span class="sxs-lookup"><span data-stu-id="a7c18-128">Yes</span></span>|<span data-ttu-id="a7c18-129">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="a7c18-129">N/A</span></span>|  
|<span data-ttu-id="a7c18-130">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="a7c18-130">password</span></span>|<span data-ttu-id="a7c18-131">Hiermee geeft u Hallo-wachtwoord van Hallo Basic referentie.</span><span class="sxs-lookup"><span data-stu-id="a7c18-131">Specifies hello password of hello Basic credential.</span></span>|<span data-ttu-id="a7c18-132">Ja</span><span class="sxs-lookup"><span data-stu-id="a7c18-132">Yes</span></span>|<span data-ttu-id="a7c18-133">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="a7c18-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="a7c18-134">Gebruik</span><span class="sxs-lookup"><span data-stu-id="a7c18-134">Usage</span></span>  
 <span data-ttu-id="a7c18-135">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="a7c18-135">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="a7c18-136">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="a7c18-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="a7c18-137">**Beleid scopes:** API</span><span class="sxs-lookup"><span data-stu-id="a7c18-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="a7c18-138"><a name="ClientCertificate"></a>Verificatie met een clientcertificaat</span><span class="sxs-lookup"><span data-stu-id="a7c18-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="a7c18-139">Gebruik Hallo `authentication-certificate` beleid tooauthenticate met een back-endservice clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="a7c18-139">Use hello `authentication-certificate` policy tooauthenticate with a backend service using client certificate.</span></span> <span data-ttu-id="a7c18-140">Hallo-certificaat moet toobe [geïnstalleerd in API Management](http://go.microsoft.com/fwlink/?LinkID=511599) eerste en wordt geïdentificeerd door de vingerafdruk.</span><span class="sxs-lookup"><span data-stu-id="a7c18-140">hello certificate needs toobe [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="a7c18-141">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="a7c18-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="a7c18-142">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="a7c18-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="a7c18-143">Elementen</span><span class="sxs-lookup"><span data-stu-id="a7c18-143">Elements</span></span>  
  
|<span data-ttu-id="a7c18-144">Naam</span><span class="sxs-lookup"><span data-stu-id="a7c18-144">Name</span></span>|<span data-ttu-id="a7c18-145">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a7c18-145">Description</span></span>|<span data-ttu-id="a7c18-146">Vereist</span><span class="sxs-lookup"><span data-stu-id="a7c18-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="a7c18-147">certificaat voor clientverificatie</span><span class="sxs-lookup"><span data-stu-id="a7c18-147">authentication-certificate</span></span>|<span data-ttu-id="a7c18-148">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="a7c18-148">Root element.</span></span>|<span data-ttu-id="a7c18-149">Ja</span><span class="sxs-lookup"><span data-stu-id="a7c18-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="a7c18-150">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="a7c18-150">Attributes</span></span>  
  
|<span data-ttu-id="a7c18-151">Naam</span><span class="sxs-lookup"><span data-stu-id="a7c18-151">Name</span></span>|<span data-ttu-id="a7c18-152">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a7c18-152">Description</span></span>|<span data-ttu-id="a7c18-153">Vereist</span><span class="sxs-lookup"><span data-stu-id="a7c18-153">Required</span></span>|<span data-ttu-id="a7c18-154">Standaard</span><span class="sxs-lookup"><span data-stu-id="a7c18-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="a7c18-155">vingerafdruk</span><span class="sxs-lookup"><span data-stu-id="a7c18-155">thumbprint</span></span>|<span data-ttu-id="a7c18-156">Hallo vingerafdruk Hallo clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="a7c18-156">hello thumbprint for hello client certificate.</span></span>|<span data-ttu-id="a7c18-157">Ja</span><span class="sxs-lookup"><span data-stu-id="a7c18-157">Yes</span></span>|<span data-ttu-id="a7c18-158">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="a7c18-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="a7c18-159">Gebruik</span><span class="sxs-lookup"><span data-stu-id="a7c18-159">Usage</span></span>  
 <span data-ttu-id="a7c18-160">Dit beleid kan worden gebruikt in het volgende beleid Hallo [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="a7c18-160">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="a7c18-161">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="a7c18-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="a7c18-162">**Beleid scopes:** API</span><span class="sxs-lookup"><span data-stu-id="a7c18-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="a7c18-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7c18-163">Next steps</span></span>
<span data-ttu-id="a7c18-164">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="a7c18-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
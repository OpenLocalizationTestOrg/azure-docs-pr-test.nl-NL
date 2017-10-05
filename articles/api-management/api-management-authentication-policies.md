---
title: Azure API Management-verificatiebeleid | Microsoft Docs
description: Meer informatie over het verificatiebeleid dat beschikbaar voor gebruik in Azure API Management.
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
ms.openlocfilehash: 63ef20a56ab7721f9ecc7025d05963cc4b0c27a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="fbab2-103">API Management-beleidsregels voor verificatie</span><span class="sxs-lookup"><span data-stu-id="fbab2-103">API Management authentication policies</span></span>
<span data-ttu-id="fbab2-104">Dit onderwerp bevat een verwijzing voor de volgende API Management-beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="fbab2-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="fbab2-105">Zie voor meer informatie over het toevoegen en configureren van beleid [-beleid in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="fbab2-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="fbab2-106"><a name="AuthenticationPolicies"></a>Verificatiebeleid</span><span class="sxs-lookup"><span data-stu-id="fbab2-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="fbab2-107">[Verificatie met Basic](api-management-authentication-policies.md#Basic) -verificatie met een back-endservice basisverificatie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fbab2-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="fbab2-108">[Verificatie met een clientcertificaat](api-management-authentication-policies.md#ClientCertificate) -verificatie met een back-endservice met behulp van clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="fbab2-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="fbab2-109"><a name="Basic"></a>Verificatie met Basic</span><span class="sxs-lookup"><span data-stu-id="fbab2-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="fbab2-110">Gebruik de `authentication-basic` beleid om te verifiëren met een back-endservice basisverificatie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fbab2-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="fbab2-111">Dit beleid wordt de HTTP-autorisatie-header effectief ingesteld op de waarde die overeenkomt met de referenties die zijn opgegeven in het beleid.</span><span class="sxs-lookup"><span data-stu-id="fbab2-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="fbab2-112">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="fbab2-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="fbab2-113">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="fbab2-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="fbab2-114">Elementen</span><span class="sxs-lookup"><span data-stu-id="fbab2-114">Elements</span></span>  
  
|<span data-ttu-id="fbab2-115">Naam</span><span class="sxs-lookup"><span data-stu-id="fbab2-115">Name</span></span>|<span data-ttu-id="fbab2-116">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fbab2-116">Description</span></span>|<span data-ttu-id="fbab2-117">Vereist</span><span class="sxs-lookup"><span data-stu-id="fbab2-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fbab2-118">verificatie-basis</span><span class="sxs-lookup"><span data-stu-id="fbab2-118">authentication-basic</span></span>|<span data-ttu-id="fbab2-119">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="fbab2-119">Root element.</span></span>|<span data-ttu-id="fbab2-120">Ja</span><span class="sxs-lookup"><span data-stu-id="fbab2-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="fbab2-121">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="fbab2-121">Attributes</span></span>  
  
|<span data-ttu-id="fbab2-122">Naam</span><span class="sxs-lookup"><span data-stu-id="fbab2-122">Name</span></span>|<span data-ttu-id="fbab2-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fbab2-123">Description</span></span>|<span data-ttu-id="fbab2-124">Vereist</span><span class="sxs-lookup"><span data-stu-id="fbab2-124">Required</span></span>|<span data-ttu-id="fbab2-125">Standaard</span><span class="sxs-lookup"><span data-stu-id="fbab2-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="fbab2-126">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="fbab2-126">username</span></span>|<span data-ttu-id="fbab2-127">Hiermee geeft u de gebruikersnaam van de algemene referentie.</span><span class="sxs-lookup"><span data-stu-id="fbab2-127">Specifies the username of the Basic credential.</span></span>|<span data-ttu-id="fbab2-128">Ja</span><span class="sxs-lookup"><span data-stu-id="fbab2-128">Yes</span></span>|<span data-ttu-id="fbab2-129">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="fbab2-129">N/A</span></span>|  
|<span data-ttu-id="fbab2-130">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="fbab2-130">password</span></span>|<span data-ttu-id="fbab2-131">Hiermee geeft u het wachtwoord van de algemene referentie.</span><span class="sxs-lookup"><span data-stu-id="fbab2-131">Specifies the password of the Basic credential.</span></span>|<span data-ttu-id="fbab2-132">Ja</span><span class="sxs-lookup"><span data-stu-id="fbab2-132">Yes</span></span>|<span data-ttu-id="fbab2-133">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="fbab2-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="fbab2-134">Gebruik</span><span class="sxs-lookup"><span data-stu-id="fbab2-134">Usage</span></span>  
 <span data-ttu-id="fbab2-135">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fbab2-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fbab2-136">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="fbab2-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="fbab2-137">**Beleid scopes:** API</span><span class="sxs-lookup"><span data-stu-id="fbab2-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="fbab2-138"><a name="ClientCertificate"></a>Verificatie met een clientcertificaat</span><span class="sxs-lookup"><span data-stu-id="fbab2-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="fbab2-139">Gebruik de `authentication-certificate` beleid om te verifiëren met een back-endservice clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="fbab2-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span></span> <span data-ttu-id="fbab2-140">Het certificaat moet worden [geïnstalleerd in API Management](http://go.microsoft.com/fwlink/?LinkID=511599) eerste en wordt geïdentificeerd door de vingerafdruk.</span><span class="sxs-lookup"><span data-stu-id="fbab2-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="fbab2-141">Beleidsverklaring</span><span class="sxs-lookup"><span data-stu-id="fbab2-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="fbab2-142">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="fbab2-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="fbab2-143">Elementen</span><span class="sxs-lookup"><span data-stu-id="fbab2-143">Elements</span></span>  
  
|<span data-ttu-id="fbab2-144">Naam</span><span class="sxs-lookup"><span data-stu-id="fbab2-144">Name</span></span>|<span data-ttu-id="fbab2-145">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fbab2-145">Description</span></span>|<span data-ttu-id="fbab2-146">Vereist</span><span class="sxs-lookup"><span data-stu-id="fbab2-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fbab2-147">certificaat voor clientverificatie</span><span class="sxs-lookup"><span data-stu-id="fbab2-147">authentication-certificate</span></span>|<span data-ttu-id="fbab2-148">Hoofdelement.</span><span class="sxs-lookup"><span data-stu-id="fbab2-148">Root element.</span></span>|<span data-ttu-id="fbab2-149">Ja</span><span class="sxs-lookup"><span data-stu-id="fbab2-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="fbab2-150">Kenmerken</span><span class="sxs-lookup"><span data-stu-id="fbab2-150">Attributes</span></span>  
  
|<span data-ttu-id="fbab2-151">Naam</span><span class="sxs-lookup"><span data-stu-id="fbab2-151">Name</span></span>|<span data-ttu-id="fbab2-152">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="fbab2-152">Description</span></span>|<span data-ttu-id="fbab2-153">Vereist</span><span class="sxs-lookup"><span data-stu-id="fbab2-153">Required</span></span>|<span data-ttu-id="fbab2-154">Standaard</span><span class="sxs-lookup"><span data-stu-id="fbab2-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="fbab2-155">vingerafdruk</span><span class="sxs-lookup"><span data-stu-id="fbab2-155">thumbprint</span></span>|<span data-ttu-id="fbab2-156">De vingerafdruk van het clientcertificaat.</span><span class="sxs-lookup"><span data-stu-id="fbab2-156">The thumbprint for the client certificate.</span></span>|<span data-ttu-id="fbab2-157">Ja</span><span class="sxs-lookup"><span data-stu-id="fbab2-157">Yes</span></span>|<span data-ttu-id="fbab2-158">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="fbab2-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="fbab2-159">Gebruik</span><span class="sxs-lookup"><span data-stu-id="fbab2-159">Usage</span></span>  
 <span data-ttu-id="fbab2-160">Dit beleid kan worden gebruikt in het volgende beleid [secties](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) en [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fbab2-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fbab2-161">**Beleid secties:** inkomende</span><span class="sxs-lookup"><span data-stu-id="fbab2-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="fbab2-162">**Beleid scopes:** API</span><span class="sxs-lookup"><span data-stu-id="fbab2-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="fbab2-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fbab2-163">Next steps</span></span>
<span data-ttu-id="fbab2-164">Zie voor meer informatie werken met beleid [-beleid in API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="fbab2-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
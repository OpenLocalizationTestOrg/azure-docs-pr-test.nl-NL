---
title: aaaSession Azure Management - Microsoft Threat Modeling Tool - | Microsoft Docs
description: oplossingen voor bedreigingen die worden weergegeven in Hallo Threat Modeling hulpprogramma
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 915ffae3f775ca6902fcfb93e7e1952ce85612f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="83ebb-103">Beveiliging Frame: Sessiebeheer | Artikelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="83ebb-104">Product/Service</span><span class="sxs-lookup"><span data-stu-id="83ebb-104">Product/Service</span></span> | <span data-ttu-id="83ebb-105">Artikel</span><span class="sxs-lookup"><span data-stu-id="83ebb-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="83ebb-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="83ebb-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="83ebb-107">De juiste afmelding implementeren met behulp van ADAL methoden bij gebruik van Azure AD</span><span class="sxs-lookup"><span data-stu-id="83ebb-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="83ebb-108">IoT-apparaat</span><span class="sxs-lookup"><span data-stu-id="83ebb-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="83ebb-109">Het gebruiken van beperkte levensduur voor gegenereerde SaS-tokens</span><span class="sxs-lookup"><span data-stu-id="83ebb-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="83ebb-110">**Azure Documentdb**</span><span class="sxs-lookup"><span data-stu-id="83ebb-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="83ebb-111">Minimale token levensduur voor tokens voor gegenereerde Resource gebruiken</span><span class="sxs-lookup"><span data-stu-id="83ebb-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="83ebb-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="83ebb-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="83ebb-113">Juiste afmelding WsFederation methoden gebruiken wanneer u AD FS implementeren</span><span class="sxs-lookup"><span data-stu-id="83ebb-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="83ebb-114">**Identiteitsserver**</span><span class="sxs-lookup"><span data-stu-id="83ebb-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="83ebb-115">Implementeren in de juiste afmelden bij gebruik van Identiteitsserver</span><span class="sxs-lookup"><span data-stu-id="83ebb-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="83ebb-116">**Webtoepassing**</span><span class="sxs-lookup"><span data-stu-id="83ebb-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="83ebb-117">Toepassingen die beschikbaar zijn via HTTPS moeten beveiligde cookies gebruiken</span><span class="sxs-lookup"><span data-stu-id="83ebb-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="83ebb-118">Alle HTTP-gebaseerde toepassing moet http alleen voor de definitie van de cookie opgeven</span><span class="sxs-lookup"><span data-stu-id="83ebb-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="83ebb-119">Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET-webpagina 's</span><span class="sxs-lookup"><span data-stu-id="83ebb-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="83ebb-120">Sessie voor inactiviteit levensduur instellen</span><span class="sxs-lookup"><span data-stu-id="83ebb-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="83ebb-121">Juiste afmelden van de toepassing hello implementeren</span><span class="sxs-lookup"><span data-stu-id="83ebb-121">Implement proper logout from hello application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="83ebb-122">**Web-API**</span><span class="sxs-lookup"><span data-stu-id="83ebb-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="83ebb-123">Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET Web-API 's</span><span class="sxs-lookup"><span data-stu-id="83ebb-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="83ebb-124"><a id="logout-adal"></a>De juiste afmelding implementeren met behulp van ADAL methoden bij gebruik van Azure AD</span><span class="sxs-lookup"><span data-stu-id="83ebb-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="83ebb-125">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-125">Title</span></span>                   | <span data-ttu-id="83ebb-126">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-127">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-127">**Component**</span></span>               | <span data-ttu-id="83ebb-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="83ebb-128">Azure AD</span></span> | 
| <span data-ttu-id="83ebb-129">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-129">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-130">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-130">Build</span></span> |  
| <span data-ttu-id="83ebb-131">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-131">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-132">Algemene</span><span class="sxs-lookup"><span data-stu-id="83ebb-132">Generic</span></span> |
| <span data-ttu-id="83ebb-133">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-133">**Attributes**</span></span>              | <span data-ttu-id="83ebb-134">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-134">N/A</span></span>  |
| <span data-ttu-id="83ebb-135">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-135">**References**</span></span>              | <span data-ttu-id="83ebb-136">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-136">N/A</span></span>  |
| <span data-ttu-id="83ebb-137">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-137">**Steps**</span></span> | <span data-ttu-id="83ebb-138">Als de toepassing hello vertrouwt op access token dat is uitgegeven door Azure AD, moet Hallo afmelding gebeurtenis-handler aanroepen</span><span class="sxs-lookup"><span data-stu-id="83ebb-138">If hello application relies on access token issued by Azure AD, hello logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="83ebb-139">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="83ebb-140">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-140">Example</span></span>
<span data-ttu-id="83ebb-141">Het moet ook de gebruikerssessie door het aanroepen van methode Session.Abandon() vernietigen.</span><span class="sxs-lookup"><span data-stu-id="83ebb-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="83ebb-142">Methode, ziet u beveiligde implementatie van de gebruiker afmelden in:</span><span class="sxs-lookup"><span data-stu-id="83ebb-142">Following method shows secure implementation of user logout:</span></span>
```C#
    [HttpPost]
        [ValidateAntiForgeryToken]
        public void LogOff()
        {
            string userObjectID = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            AuthenticationContext authContext = new AuthenticationContext(Authority + TenantId, new NaiveSessionCache(userObjectID));
            authContext.TokenCache.Clear();
            Session.Clear();
            Session.Abandon();
            Response.SetCookie(new HttpCookie("ASP.NET_SessionId", string.Empty));
            HttpContext.GetOwinContext().Authentication.SignOut(
                OpenIdConnectAuthenticationDefaults.AuthenticationType,
                CookieAuthenticationDefaults.AuthenticationType);
        } 
```

## <span data-ttu-id="83ebb-143"><a id="finite-tokens"></a>Het gebruiken van beperkte levensduur voor gegenereerde SaS-tokens</span><span class="sxs-lookup"><span data-stu-id="83ebb-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="83ebb-144">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-144">Title</span></span>                   | <span data-ttu-id="83ebb-145">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-146">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-146">**Component**</span></span>               | <span data-ttu-id="83ebb-147">IoT-apparaat</span><span class="sxs-lookup"><span data-stu-id="83ebb-147">IoT Device</span></span> | 
| <span data-ttu-id="83ebb-148">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-148">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-149">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-149">Build</span></span> |  
| <span data-ttu-id="83ebb-150">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-150">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-151">Algemene</span><span class="sxs-lookup"><span data-stu-id="83ebb-151">Generic</span></span> |
| <span data-ttu-id="83ebb-152">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-152">**Attributes**</span></span>              | <span data-ttu-id="83ebb-153">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-153">N/A</span></span>  |
| <span data-ttu-id="83ebb-154">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-154">**References**</span></span>              | <span data-ttu-id="83ebb-155">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-155">N/A</span></span>  |
| <span data-ttu-id="83ebb-156">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-156">**Steps**</span></span> | <span data-ttu-id="83ebb-157">SaS-tokens gegenereerd voor het verifiëren van tooAzure IoT Hub moeten een eindige verloopperiode hebben.</span><span class="sxs-lookup"><span data-stu-id="83ebb-157">SaS tokens generated for authenticating tooAzure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="83ebb-158">Houd Hallo SaS token levensduur tooa minimale toolimit Hallo hoeveelheid tijd die kan worden cookies geval Hallo tokens worden getroffen.</span><span class="sxs-lookup"><span data-stu-id="83ebb-158">Keep hello SaS token lifetimes tooa minimum toolimit hello amount of time they can be replayed in case hello tokens are compromised.</span></span>|

## <span data-ttu-id="83ebb-159"><a id="resource-tokens"></a>Minimale token levensduur voor tokens voor gegenereerde Resource gebruiken</span><span class="sxs-lookup"><span data-stu-id="83ebb-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="83ebb-160">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-160">Title</span></span>                   | <span data-ttu-id="83ebb-161">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-162">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-162">**Component**</span></span>               | <span data-ttu-id="83ebb-163">Azure Documentdb</span><span class="sxs-lookup"><span data-stu-id="83ebb-163">Azure Document DB</span></span> | 
| <span data-ttu-id="83ebb-164">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-164">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-165">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-165">Build</span></span> |  
| <span data-ttu-id="83ebb-166">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-166">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-167">Algemene</span><span class="sxs-lookup"><span data-stu-id="83ebb-167">Generic</span></span> |
| <span data-ttu-id="83ebb-168">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-168">**Attributes**</span></span>              | <span data-ttu-id="83ebb-169">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-169">N/A</span></span>  |
| <span data-ttu-id="83ebb-170">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-170">**References**</span></span>              | <span data-ttu-id="83ebb-171">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-171">N/A</span></span>  |
| <span data-ttu-id="83ebb-172">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-172">**Steps**</span></span> | <span data-ttu-id="83ebb-173">Reduceren timespan Hallo van resource token tooa voorgeschreven minimumwaarde.</span><span class="sxs-lookup"><span data-stu-id="83ebb-173">Reduce hello timespan of resource token tooa minimum value required.</span></span> <span data-ttu-id="83ebb-174">Resource-tokens hebben een geldige timespan standaardwaarde van 1 uur.</span><span class="sxs-lookup"><span data-stu-id="83ebb-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="83ebb-175"><a id="wsfederation-logout"></a>Juiste afmelding WsFederation methoden gebruiken wanneer u AD FS implementeren</span><span class="sxs-lookup"><span data-stu-id="83ebb-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="83ebb-176">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-176">Title</span></span>                   | <span data-ttu-id="83ebb-177">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-178">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-178">**Component**</span></span>               | <span data-ttu-id="83ebb-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="83ebb-179">ADFS</span></span> | 
| <span data-ttu-id="83ebb-180">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-180">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-181">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-181">Build</span></span> |  
| <span data-ttu-id="83ebb-182">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-182">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-183">Algemene</span><span class="sxs-lookup"><span data-stu-id="83ebb-183">Generic</span></span> |
| <span data-ttu-id="83ebb-184">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-184">**Attributes**</span></span>              | <span data-ttu-id="83ebb-185">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-185">N/A</span></span>  |
| <span data-ttu-id="83ebb-186">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-186">**References**</span></span>              | <span data-ttu-id="83ebb-187">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-187">N/A</span></span>  |
| <span data-ttu-id="83ebb-188">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-188">**Steps**</span></span> | <span data-ttu-id="83ebb-189">Als de toepassing hello STS token dat is uitgegeven door AD FS, moet Hallo afmelding gebeurtenis-handler WSFederationAuthenticationModule.FederatedSignOut() methode toolog uit Hallo gebruiker aanroepen.</span><span class="sxs-lookup"><span data-stu-id="83ebb-189">If hello application relies on STS token issued by ADFS, hello logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method toolog out hello user.</span></span> <span data-ttu-id="83ebb-190">Ook Hallo huidige sessie moet worden vernietigd en Hallo token-outwaarde voor sessies te herstellen en geneutraliseerd.</span><span class="sxs-lookup"><span data-stu-id="83ebb-190">Also hello current session should be destroyed, and hello session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="83ebb-191">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes hello user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at hello specified security token service (STS) by using hello WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of hello current session and raises hello appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at hello specified security token service (STS) by using hello WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="83ebb-192"><a id="proper-logout"></a>Implementeren in de juiste afmelden bij gebruik van Identiteitsserver</span><span class="sxs-lookup"><span data-stu-id="83ebb-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="83ebb-193">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-193">Title</span></span>                   | <span data-ttu-id="83ebb-194">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-195">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-195">**Component**</span></span>               | <span data-ttu-id="83ebb-196">Identiteitsserver</span><span class="sxs-lookup"><span data-stu-id="83ebb-196">Identity Server</span></span> | 
| <span data-ttu-id="83ebb-197">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-197">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-198">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-198">Build</span></span> |  
| <span data-ttu-id="83ebb-199">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-199">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-200">Algemene</span><span class="sxs-lookup"><span data-stu-id="83ebb-200">Generic</span></span> |
| <span data-ttu-id="83ebb-201">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-201">**Attributes**</span></span>              | <span data-ttu-id="83ebb-202">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-202">N/A</span></span>  |
| <span data-ttu-id="83ebb-203">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-203">**References**</span></span>              | [<span data-ttu-id="83ebb-204">IdentityServer3 federatieve afmelden</span><span class="sxs-lookup"><span data-stu-id="83ebb-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="83ebb-205">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-205">**Steps**</span></span> | <span data-ttu-id="83ebb-206">IdentityServer ondersteunt Hallo mogelijkheid toofederate met externe id-providers.</span><span class="sxs-lookup"><span data-stu-id="83ebb-206">IdentityServer supports hello ability toofederate with external identity providers.</span></span> <span data-ttu-id="83ebb-207">Wanneer een gebruiker zich afmeldt een upstream-id-provider, kan afhankelijk van het Hallo-protocol gebruikt, dit worden mogelijk tooreceive een melding wanneer Hallo gebruiker zich afmeldt. Kunt u IdentityServer toonotify clients zodat ze kunnen ook zich Hallo gebruiker uit. Raadpleeg de documentatie Hallo in Hallo verwijzingen gedeelte voor het Hallo-implementatiegegevens.</span><span class="sxs-lookup"><span data-stu-id="83ebb-207">When a user signs out of an upstream identity provider, depending upon hello protocol used, it might be possible tooreceive a notification when hello user signs out. It allows IdentityServer toonotify its clients so they can also sign hello user out. Check hello documentation in hello references section for hello implementation details.</span></span>|

## <span data-ttu-id="83ebb-208"><a id="https-secure-cookies"></a>Toepassingen die beschikbaar zijn via HTTPS moeten beveiligde cookies gebruiken</span><span class="sxs-lookup"><span data-stu-id="83ebb-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="83ebb-209">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-209">Title</span></span>                   | <span data-ttu-id="83ebb-210">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-211">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-211">**Component**</span></span>               | <span data-ttu-id="83ebb-212">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83ebb-212">Web Application</span></span> | 
| <span data-ttu-id="83ebb-213">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-213">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-214">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-214">Build</span></span> |  
| <span data-ttu-id="83ebb-215">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-215">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-216">Algemene</span><span class="sxs-lookup"><span data-stu-id="83ebb-216">Generic</span></span> |
| <span data-ttu-id="83ebb-217">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-217">**Attributes**</span></span>              | <span data-ttu-id="83ebb-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="83ebb-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="83ebb-219">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-219">**References**</span></span>              | <span data-ttu-id="83ebb-220">[httpCookies Element (ASP.NET-instellingenschema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure-eigenschap](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="83ebb-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="83ebb-221">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-221">**Steps**</span></span> | <span data-ttu-id="83ebb-222">Cookies zijn normaal gesproken alleen toegankelijk toohello domein waarvoor ze zijn binnen het bereik.</span><span class="sxs-lookup"><span data-stu-id="83ebb-222">Cookies are normally only accessible toohello domain for which they were scoped.</span></span> <span data-ttu-id="83ebb-223">Helaas bevat Hallo definitie van 'domein' geen Hallo protocol zodat cookies die zijn gemaakt via HTTPS toegankelijk via HTTP zijn.</span><span class="sxs-lookup"><span data-stu-id="83ebb-223">Unfortunately, hello definition of "domain" does not include hello protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="83ebb-224">Hallo "veilig" kenmerk geeft aan toohello browser die cookie Hallo alleen beschikbaar moet worden gesteld via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="83ebb-224">hello "secure" attribute indicates toohello browser that hello cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="83ebb-225">Zorg dat alle cookies instellen via HTTPS Hallo gebruikt **beveiligde** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="83ebb-225">Ensure that all cookies set over HTTPS use hello **secure** attribute.</span></span> <span data-ttu-id="83ebb-226">Hallo-vereiste kan worden afgedwongen in Hallo web.config-bestand door Hallo requireSSL kenmerk tootrue instellen.</span><span class="sxs-lookup"><span data-stu-id="83ebb-226">hello requirement can be enforced in hello web.config file by setting hello requireSSL attribute tootrue.</span></span> <span data-ttu-id="83ebb-227">Hallo benadering de voorkeur omdat deze Hallo zal geforceerd is **beveiligde** kenmerk voor alle huidige en toekomstige cookies zonder Hallo nodig toomake extra codewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="83ebb-227">It is hello preferred approach because it will enforce hello **secure** attribute for all current and future cookies without hello need toomake any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="83ebb-228">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="83ebb-229">Hallo-instelling wordt afgedwongen, zelfs als HTTP gebruikte tooaccess Hallo-toepassing is.</span><span class="sxs-lookup"><span data-stu-id="83ebb-229">hello setting is enforced even if HTTP is used tooaccess hello application.</span></span> <span data-ttu-id="83ebb-230">Als u HTTP gebruikt tooaccess Hallo toepassing, hello instelling einden Hallo toepassing omdat Hallo cookies worden ingesteld met Hallo beveiligde kenmerk en het Hallo-browser niet deze verstuurt back-toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="83ebb-230">If HTTP is used tooaccess hello application, hello setting breaks hello application because hello cookies are set with hello secure attribute and hello browser will not send them back toohello application.</span></span>

| <span data-ttu-id="83ebb-231">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-231">Title</span></span>                   | <span data-ttu-id="83ebb-232">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-233">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-233">**Component**</span></span>               | <span data-ttu-id="83ebb-234">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83ebb-234">Web Application</span></span> | 
| <span data-ttu-id="83ebb-235">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-235">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-236">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-236">Build</span></span> |  
| <span data-ttu-id="83ebb-237">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-237">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-238">Webformulieren, MVC5</span><span class="sxs-lookup"><span data-stu-id="83ebb-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="83ebb-239">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-239">**Attributes**</span></span>              | <span data-ttu-id="83ebb-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="83ebb-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="83ebb-241">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-241">**References**</span></span>              | <span data-ttu-id="83ebb-242">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-242">N/A</span></span>  |
| <span data-ttu-id="83ebb-243">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-243">**Steps**</span></span> | <span data-ttu-id="83ebb-244">Wanneer Hallo-webtoepassing is Hallo Relying Party en Hallo IdP ADFS-server is, Hallo FedAuth-token van beveiligde kenmerk kan worden geconfigureerd met requireSSL tooTrue instellen in `system.identityModel.services` sectie van web.config:</span><span class="sxs-lookup"><span data-stu-id="83ebb-244">When hello web application is hello Relying Party, and hello IdP is ADFS server, hello FedAuth token's secure attribute can be configured by setting requireSSL tooTrue in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="83ebb-245">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="83ebb-246"><a id="cookie-definition"></a>Alle HTTP-gebaseerde toepassing moet http alleen voor de definitie van de cookie opgeven</span><span class="sxs-lookup"><span data-stu-id="83ebb-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="83ebb-247">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-247">Title</span></span>                   | <span data-ttu-id="83ebb-248">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-249">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-249">**Component**</span></span>               | <span data-ttu-id="83ebb-250">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83ebb-250">Web Application</span></span> | 
| <span data-ttu-id="83ebb-251">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-251">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-252">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-252">Build</span></span> |  
| <span data-ttu-id="83ebb-253">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-253">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-254">Algemene</span><span class="sxs-lookup"><span data-stu-id="83ebb-254">Generic</span></span> |
| <span data-ttu-id="83ebb-255">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-255">**Attributes**</span></span>              | <span data-ttu-id="83ebb-256">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-256">N/A</span></span>  |
| <span data-ttu-id="83ebb-257">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-257">**References**</span></span>              | [<span data-ttu-id="83ebb-258">Beveiligde Cookie-kenmerk</span><span class="sxs-lookup"><span data-stu-id="83ebb-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="83ebb-259">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-259">**Steps**</span></span> | <span data-ttu-id="83ebb-260">toomitigate hello gevaar voor openbaarmaking met een aanval cross-site scripting (XSS), een nieuw kenmerk - httpOnly - geïntroduceerd toocookies is en wordt ondersteund door alle belangrijke browsers.</span><span class="sxs-lookup"><span data-stu-id="83ebb-260">toomitigate hello risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced toocookies and is supported by all major browsers.</span></span> <span data-ttu-id="83ebb-261">Hallo-kenmerk bevat een cookie is niet toegankelijk via script.</span><span class="sxs-lookup"><span data-stu-id="83ebb-261">hello attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="83ebb-262">Met behulp van cookies HttpOnly verkleint een webtoepassing Hallo kans dat gevoelige informatie in Hallo cookie kan worden gestolen via scripts en website tooan kwaadwillende persoon verzonden.</span><span class="sxs-lookup"><span data-stu-id="83ebb-262">By using HttpOnly cookies, a web application reduces hello possibility that sensitive information contained in hello cookie can be stolen via script and sent tooan attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="83ebb-263">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-263">Example</span></span>
<span data-ttu-id="83ebb-264">Alle HTTP-gebaseerde toepassingen die gebruikmaken van cookies moeten HttpOnly opgeven in de definitie van de cookie hello, door het implementeren van na de configuratie in web.config:</span><span class="sxs-lookup"><span data-stu-id="83ebb-264">All HTTP-based applications that use cookies should specify HttpOnly in hello cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="83ebb-265">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-265">Title</span></span>                   | <span data-ttu-id="83ebb-266">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-267">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-267">**Component**</span></span>               | <span data-ttu-id="83ebb-268">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83ebb-268">Web Application</span></span> | 
| <span data-ttu-id="83ebb-269">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-269">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-270">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-270">Build</span></span> |  
| <span data-ttu-id="83ebb-271">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-271">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-272">Web Forms</span><span class="sxs-lookup"><span data-stu-id="83ebb-272">Web Forms</span></span> |
| <span data-ttu-id="83ebb-273">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-273">**Attributes**</span></span>              | <span data-ttu-id="83ebb-274">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-274">N/A</span></span>  |
| <span data-ttu-id="83ebb-275">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-275">**References**</span></span>              | [<span data-ttu-id="83ebb-276">De eigenschap FormsAuthentication.RequireSSL</span><span class="sxs-lookup"><span data-stu-id="83ebb-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="83ebb-277">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-277">**Steps**</span></span> | <span data-ttu-id="83ebb-278">Hallo RequireSSL eigenschapswaarde wordt ingesteld op Hallo-configuratiebestand voor een ASP.NET-toepassing met behulp van Hallo requireSSL kenmerk van het Hallo-configuratie-element.</span><span class="sxs-lookup"><span data-stu-id="83ebb-278">hello RequireSSL property value is set in hello configuration file for an ASP.NET application by using hello requireSSL attribute of hello configuration element.</span></span> <span data-ttu-id="83ebb-279">U kunt opgeven in Hallo Web.config-bestand voor uw ASP.NET-toepassing of SSL (Secure Sockets Layer) vereist tooreturn Hallo formulierverificatie cookie toohello server door instelling Hallo requireSSL kenmerk is.</span><span class="sxs-lookup"><span data-stu-id="83ebb-279">You can specify in hello Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required tooreturn hello forms-authentication cookie toohello server by setting hello requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="83ebb-280">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-280">Example</span></span> 
<span data-ttu-id="83ebb-281">Hallo stelt volgende codevoorbeeld Hallo requireSSL-kenmerk in Hallo Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="83ebb-281">hello following code example sets hello requireSSL attribute in hello Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="83ebb-282">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-282">Title</span></span>                   | <span data-ttu-id="83ebb-283">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-284">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-284">**Component**</span></span>               | <span data-ttu-id="83ebb-285">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83ebb-285">Web Application</span></span> | 
| <span data-ttu-id="83ebb-286">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-286">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-287">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-287">Build</span></span> |  
| <span data-ttu-id="83ebb-288">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-288">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="83ebb-289">MVC5</span></span> |
| <span data-ttu-id="83ebb-290">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-290">**Attributes**</span></span>              | <span data-ttu-id="83ebb-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="83ebb-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="83ebb-292">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-292">**References**</span></span>              | [<span data-ttu-id="83ebb-293">Configuratie van Windows Identity Foundation (WIF) – deel II</span><span class="sxs-lookup"><span data-stu-id="83ebb-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="83ebb-294">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-294">**Steps**</span></span> | <span data-ttu-id="83ebb-295">tooset httpOnly kenmerk voor FedAuth cookies, hideFromCsript kenmerkwaarde moet worden ingesteld tooTrue hebben.</span><span class="sxs-lookup"><span data-stu-id="83ebb-295">tooset httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set tooTrue.</span></span> |

### <a name="example"></a><span data-ttu-id="83ebb-296">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-296">Example</span></span>
<span data-ttu-id="83ebb-297">Volgende configuratie ziet u de juiste configuratie Hallo:</span><span class="sxs-lookup"><span data-stu-id="83ebb-297">Following configuration shows hello correct configuration:</span></span>
```XML
<federatedAuthentication>
<cookieHandler mode="Custom"
                       hideFromScript="true"
                       name="FedAuth"
                       path="/"
                       requireSsl="true"
                       persistentSessionLifetime="25">
</cookieHandler>
</federatedAuthentication>
```

## <span data-ttu-id="83ebb-298"><a id="csrf-asp"></a>Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET-webpagina 's</span><span class="sxs-lookup"><span data-stu-id="83ebb-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="83ebb-299">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-299">Title</span></span>                   | <span data-ttu-id="83ebb-300">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-301">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-301">**Component**</span></span>               | <span data-ttu-id="83ebb-302">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83ebb-302">Web Application</span></span> | 
| <span data-ttu-id="83ebb-303">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-303">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-304">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-304">Build</span></span> |  
| <span data-ttu-id="83ebb-305">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-305">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-306">Algemene</span><span class="sxs-lookup"><span data-stu-id="83ebb-306">Generic</span></span> |
| <span data-ttu-id="83ebb-307">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-307">**Attributes**</span></span>              | <span data-ttu-id="83ebb-308">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-308">N/A</span></span>  |
| <span data-ttu-id="83ebb-309">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-309">**References**</span></span>              | <span data-ttu-id="83ebb-310">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-310">N/A</span></span>  |
| <span data-ttu-id="83ebb-311">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-311">**Steps**</span></span> | <span data-ttu-id="83ebb-312">Aanvraagvervalsing op meerdere sites (CSRF of XSRF) is een type van een aanval waarbij een aanvaller acties in de beveiligingscontext Hallo van vastgestelde sessie een andere gebruiker op een website kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="83ebb-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="83ebb-313">Hallo-doel is toomodify of inhoud verwijderen als gerichte website Hallo afhankelijk is uitsluitend van cookies tooauthenticate ontvangen verzoek om sessie.</span><span class="sxs-lookup"><span data-stu-id="83ebb-313">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="83ebb-314">Een aanvaller kan deze kwetsbaarheid misbruiken door een andere gebruiker browser tooload een URL met een opdracht van een kwetsbaar site waarop Hallo gebruiker is al aangemeld.</span><span class="sxs-lookup"><span data-stu-id="83ebb-314">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="83ebb-315">Er zijn veel manieren voor een aanvaller toodo dat, zoals door het hosten van een andere website die wordt geladen een resource van kwetsbare Hallo-server of ophalen Hallo gebruiker tooclick een koppeling.</span><span class="sxs-lookup"><span data-stu-id="83ebb-315">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="83ebb-316">Hallo-aanval kan worden voorkomen als Hallo-server stuurt de client van een extra token toohello, vereist Hallo client tooinclude dat token in alle toekomstige aanvragen en verifieert dat alle toekomstige aanvragen een token dat betrekking heeft toohello huidige sessie bevatten, zoals door met behulp van ASP.NET AntiForgeryToken Hallo of ViewState.</span><span class="sxs-lookup"><span data-stu-id="83ebb-316">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="83ebb-317">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-317">Title</span></span>                   | <span data-ttu-id="83ebb-318">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-319">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-319">**Component**</span></span>               | <span data-ttu-id="83ebb-320">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83ebb-320">Web Application</span></span> | 
| <span data-ttu-id="83ebb-321">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-321">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-322">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-322">Build</span></span> |  
| <span data-ttu-id="83ebb-323">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-323">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="83ebb-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="83ebb-325">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-325">**Attributes**</span></span>              | <span data-ttu-id="83ebb-326">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-326">N/A</span></span>  |
| <span data-ttu-id="83ebb-327">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-327">**References**</span></span>              | [<span data-ttu-id="83ebb-328">XSRF/CSRF voorkomen in ASP.NET MVC en webpagina 's</span><span class="sxs-lookup"><span data-stu-id="83ebb-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="83ebb-329">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-329">**Steps**</span></span> | <span data-ttu-id="83ebb-330">Formulieren anti-CSRF en ASP.NET MVC - gebruik Hallo `AntiForgeryToken` Help-methode op weergaven; put een `Html.AntiForgeryToken()` in Hallo formulier, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="83ebb-330">Anti-CSRF and ASP.NET MVC forms - Use hello `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into hello form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="83ebb-331">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="83ebb-332">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="83ebb-333">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-333">Example</span></span>
<span data-ttu-id="83ebb-334">Op Hallo dezelfde tijdstip, Html.AntiForgeryToken() biedt Hallo bezoeker een cookie aangeroepen __RequestVerificationToken Hello dezelfde als Hallo willekeurige verborgen waarde waarde hierboven weergegeven.</span><span class="sxs-lookup"><span data-stu-id="83ebb-334">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="83ebb-335">Vervolgens voegt u toovalidate een binnenkomende Formulierbericht Hallo [ValidateAntiForgeryToken] filter toohello doel-actiemethode.</span><span class="sxs-lookup"><span data-stu-id="83ebb-335">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="83ebb-336">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="83ebb-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="83ebb-337">Autorisatiefilter die of controleert:</span><span class="sxs-lookup"><span data-stu-id="83ebb-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="83ebb-338">Hallo binnenkomende aanvraag heeft een cookie met de naam __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="83ebb-338">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="83ebb-339">Hallo binnenkomende aanvraag heeft een `Request.Form` vermelding __RequestVerificationToken aangeroepen</span><span class="sxs-lookup"><span data-stu-id="83ebb-339">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="83ebb-340">Deze cookie en `Request.Form` waarden overeenkomen, ervan uitgaande dat alle goed is, doorloopt NTDS Hallo-aanvraag die normaal werken.</span><span class="sxs-lookup"><span data-stu-id="83ebb-340">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="83ebb-341">Maar als dit niet het geval is, klikt u vervolgens een Autorisatiefout met het bericht 'een vereiste anti-vervalsingstoken is niet opgegeven of is ongeldig'.</span><span class="sxs-lookup"><span data-stu-id="83ebb-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="83ebb-342">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-342">Example</span></span>
<span data-ttu-id="83ebb-343">Anti-CSRF en AJAX: Hallo formulier token kan een probleem voor AJAX-aanvragen worden, omdat een AJAX-aanvraag JSON-gegevens, geen HTML-formuliergegevens kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="83ebb-343">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="83ebb-344">Eén oplossing is toosend Hallo tokens in een aangepaste HTTP-header.</span><span class="sxs-lookup"><span data-stu-id="83ebb-344">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="83ebb-345">Hallo volgende code gebruikt Razor syntaxis toogenerate Hallo tokens en vervolgens voegt Hallo tokens tooan AJAX-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="83ebb-345">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> 
```C#
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }

    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="83ebb-346">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-346">Example</span></span>
<span data-ttu-id="83ebb-347">Wanneer u Hallo aanvraag verwerkt, moet u Hallo tokens extraheren uit de aanvraagheader Hallo.</span><span class="sxs-lookup"><span data-stu-id="83ebb-347">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="83ebb-348">Vervolgens roept Hallo AntiForgery.Validate methode toovalidate Hallo tokens.</span><span class="sxs-lookup"><span data-stu-id="83ebb-348">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="83ebb-349">Hallo methode Validate genereert een uitzondering als Hallo tokens niet geldig zijn.</span><span class="sxs-lookup"><span data-stu-id="83ebb-349">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

| <span data-ttu-id="83ebb-350">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-350">Title</span></span>                   | <span data-ttu-id="83ebb-351">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-352">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-352">**Component**</span></span>               | <span data-ttu-id="83ebb-353">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83ebb-353">Web Application</span></span> | 
| <span data-ttu-id="83ebb-354">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-354">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-355">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-355">Build</span></span> |  
| <span data-ttu-id="83ebb-356">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-356">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-357">Web Forms</span><span class="sxs-lookup"><span data-stu-id="83ebb-357">Web Forms</span></span> |
| <span data-ttu-id="83ebb-358">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-358">**Attributes**</span></span>              | <span data-ttu-id="83ebb-359">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-359">N/A</span></span>  |
| <span data-ttu-id="83ebb-360">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-360">**References**</span></span>              | [<span data-ttu-id="83ebb-361">Los het voordeel van ASP.NET ingebouwde functies tooFend uit Web-aanvallen</span><span class="sxs-lookup"><span data-stu-id="83ebb-361">Take Advantage of ASP.NET Built-in Features tooFend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="83ebb-362">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-362">**Steps**</span></span> | <span data-ttu-id="83ebb-363">CSRF aanvallen in het webformulier op basis van toepassingen kunnen worden verminderd door het instellen van ViewStateUserKey tooa willekeurige tekenreeks varieert voor elke gebruiker - gebruikers-ID of beter nog sessie-id.</span><span class="sxs-lookup"><span data-stu-id="83ebb-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey tooa random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="83ebb-364">Sessie-ID is veel beter geschikt zijn voor een aantal technische en sociale oorzaken hebben, omdat een sessie-ID onvoorspelbare, is een time-out optreedt en varieert op basis van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="83ebb-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="83ebb-365">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-365">Example</span></span>
<span data-ttu-id="83ebb-366">Dit is Hallo-code die u nodig hebt toohave in alle pagina's:</span><span class="sxs-lookup"><span data-stu-id="83ebb-366">Here's hello code you need toohave in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="83ebb-367"><a id="inactivity-lifetime"></a>Sessie voor inactiviteit levensduur instellen</span><span class="sxs-lookup"><span data-stu-id="83ebb-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="83ebb-368">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-368">Title</span></span>                   | <span data-ttu-id="83ebb-369">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-370">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-370">**Component**</span></span>               | <span data-ttu-id="83ebb-371">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83ebb-371">Web Application</span></span> | 
| <span data-ttu-id="83ebb-372">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-372">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-373">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-373">Build</span></span> |  
| <span data-ttu-id="83ebb-374">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-374">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-375">Algemene</span><span class="sxs-lookup"><span data-stu-id="83ebb-375">Generic</span></span> |
| <span data-ttu-id="83ebb-376">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-376">**Attributes**</span></span>              | <span data-ttu-id="83ebb-377">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-377">N/A</span></span>  |
| <span data-ttu-id="83ebb-378">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-378">**References**</span></span>              | <span data-ttu-id="83ebb-379">[De eigenschap HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="83ebb-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="83ebb-380">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-380">**Steps**</span></span> | <span data-ttu-id="83ebb-381">Sessietime-out vertegenwoordigt Hallo gebeurtenis voordoet wanneer een gebruiker niet voert geen actie op een website tijdens een interval van (gedefinieerd door de webserver).</span><span class="sxs-lookup"><span data-stu-id="83ebb-381">Session timeout represents hello event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="83ebb-382">Hallo gebeurtenis aan serverzijde, Hallo Wijzigingsstatus van Hallo gebruiker sessie too'invalid' (bijvoorbeeld ' niet meer gebruikt') en Hallo web server toodestroy krijgt deze de instructie (verwijderen van alle gegevens die zijn opgenomen in de App).</span><span class="sxs-lookup"><span data-stu-id="83ebb-382">hello event, on server side, change hello status of hello user session too'invalid' (for example  "not used anymore") and instruct hello web server toodestroy it (deleting all data contained into it).</span></span> <span data-ttu-id="83ebb-383">Hallo stelt volgende codevoorbeeld Hallo time-out sessie kenmerk too15 minuten in Hallo Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="83ebb-383">hello following code example sets hello timeout session attribute too15 minutes in hello Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="83ebb-384">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-384">Example</span></span>
<span data-ttu-id="83ebb-385">'''XML-code <configuration> < system.web > <sessionState mode="InProc" cookieless="true" timeout="15" /> < /system.web ></configuration></span><span class="sxs-lookup"><span data-stu-id="83ebb-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="83ebb-386">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-386">Title</span></span>                   | <span data-ttu-id="83ebb-387">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-388">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-388">**Component**</span></span>               | <span data-ttu-id="83ebb-389">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83ebb-389">Web Application</span></span> | 
| <span data-ttu-id="83ebb-390">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-390">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-391">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-391">Build</span></span> |  
| <span data-ttu-id="83ebb-392">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-392">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-393">Web Forms</span><span class="sxs-lookup"><span data-stu-id="83ebb-393">Web Forms</span></span> |
| <span data-ttu-id="83ebb-394">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-394">**Attributes**</span></span>              | <span data-ttu-id="83ebb-395">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-395">N/A</span></span>  |
| <span data-ttu-id="83ebb-396">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-396">**References**</span></span>              | <span data-ttu-id="83ebb-397">[Element vormt voor verificatie (ASP.NET-instellingenschema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="83ebb-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="83ebb-398">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-398">**Steps**</span></span> | <span data-ttu-id="83ebb-399">Hallo Formulierverificatieticket cookie time-out too15 minuten instellen</span><span class="sxs-lookup"><span data-stu-id="83ebb-399">Set hello Forms Authentication Ticket cookie timeout too15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="83ebb-400">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-400">Example</span></span>
<span data-ttu-id="83ebb-401">'''XML-code<forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="83ebb-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When hello web application is Relying Party and ADFS is hello STS, hello lifetime of hello authentication cookies - FedAuth tokens - can be set by hello following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use hello code below tooenable encryption-decryption of claims received from ADFS. Thumbprint value varies based on hello certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="83ebb-402">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-402">Example</span></span>
<span data-ttu-id="83ebb-403">Ook Hallo levensduur van token SAML-claim uitgegeven AD FS moet worden ingesteld op too15 minuten, door het uitvoeren van de volgende powershell-opdracht op de ADFS-server Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="83ebb-403">Also hello ADFS issued SAML claim token's lifetime should be set too15 minutes, by executing hello following powershell command on hello ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="83ebb-404"><a id="proper-app-logout"></a>Juiste afmelden van de toepassing hello implementeren</span><span class="sxs-lookup"><span data-stu-id="83ebb-404"><a id="proper-app-logout"></a>Implement proper logout from hello application</span></span>

| <span data-ttu-id="83ebb-405">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-405">Title</span></span>                   | <span data-ttu-id="83ebb-406">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-407">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-407">**Component**</span></span>               | <span data-ttu-id="83ebb-408">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="83ebb-408">Web Application</span></span> | 
| <span data-ttu-id="83ebb-409">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-409">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-410">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-410">Build</span></span> |  
| <span data-ttu-id="83ebb-411">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-411">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-412">Algemene</span><span class="sxs-lookup"><span data-stu-id="83ebb-412">Generic</span></span> |
| <span data-ttu-id="83ebb-413">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-413">**Attributes**</span></span>              | <span data-ttu-id="83ebb-414">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-414">N/A</span></span>  |
| <span data-ttu-id="83ebb-415">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-415">**References**</span></span>              | <span data-ttu-id="83ebb-416">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-416">N/A</span></span>  |
| <span data-ttu-id="83ebb-417">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-417">**Steps**</span></span> | <span data-ttu-id="83ebb-418">Uitvoeren juiste afmelden van de toepassing hello, als de gebruiker op drukt knop Afmelden.</span><span class="sxs-lookup"><span data-stu-id="83ebb-418">Perform proper Sign Out from hello application, when user presses log out button.</span></span> <span data-ttu-id="83ebb-419">Bij het afmelden, moet toepassing vernietigen gebruikerssessie, en ook opnieuw instellen en cookie-outwaarde voor sessies, samen met opnieuw instellen en de waarde van de cookie verificatie nullifying ongeldig verklaard.</span><span class="sxs-lookup"><span data-stu-id="83ebb-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="83ebb-420">Ook wanneer meerdere sessies gebonden tooa één gebruikersidentiteit zijn, moeten ze worden gezamenlijk afgesloten aan de serverzijde Hallo op time-out of meld u af.</span><span class="sxs-lookup"><span data-stu-id="83ebb-420">Also, when multiple sessions are tied tooa single user identity, they must be collectively terminated on hello server side at timeout or logout.</span></span> <span data-ttu-id="83ebb-421">Ten slotte zorgen ervoor dat afmelding functionaliteit beschikbaar op elke pagina.</span><span class="sxs-lookup"><span data-stu-id="83ebb-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="83ebb-422"><a id="csrf-api"></a>Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET Web-API 's</span><span class="sxs-lookup"><span data-stu-id="83ebb-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="83ebb-423">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-423">Title</span></span>                   | <span data-ttu-id="83ebb-424">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-425">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-425">**Component**</span></span>               | <span data-ttu-id="83ebb-426">Web-API</span><span class="sxs-lookup"><span data-stu-id="83ebb-426">Web API</span></span> | 
| <span data-ttu-id="83ebb-427">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-427">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-428">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-428">Build</span></span> |  
| <span data-ttu-id="83ebb-429">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-429">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-430">Algemene</span><span class="sxs-lookup"><span data-stu-id="83ebb-430">Generic</span></span> |
| <span data-ttu-id="83ebb-431">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-431">**Attributes**</span></span>              | <span data-ttu-id="83ebb-432">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-432">N/A</span></span>  |
| <span data-ttu-id="83ebb-433">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-433">**References**</span></span>              | <span data-ttu-id="83ebb-434">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-434">N/A</span></span>  |
| <span data-ttu-id="83ebb-435">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-435">**Steps**</span></span> | <span data-ttu-id="83ebb-436">Aanvraagvervalsing op meerdere sites (CSRF of XSRF) is een type van een aanval waarbij een aanvaller acties in de beveiligingscontext Hallo van vastgestelde sessie een andere gebruiker op een website kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="83ebb-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in hello security context of a different user's established session on a web site.</span></span> <span data-ttu-id="83ebb-437">Hallo-doel is toomodify of inhoud verwijderen als gerichte website Hallo afhankelijk is uitsluitend van cookies tooauthenticate ontvangen verzoek om sessie.</span><span class="sxs-lookup"><span data-stu-id="83ebb-437">hello goal is toomodify or delete content, if hello targeted web site relies exclusively on session cookies tooauthenticate received request.</span></span> <span data-ttu-id="83ebb-438">Een aanvaller kan deze kwetsbaarheid misbruiken door een andere gebruiker browser tooload een URL met een opdracht van een kwetsbaar site waarop Hallo gebruiker is al aangemeld.</span><span class="sxs-lookup"><span data-stu-id="83ebb-438">An attacker could exploit this vulnerability by getting a different user's browser tooload a URL with a command from a vulnerable site on which hello user is already logged in.</span></span> <span data-ttu-id="83ebb-439">Er zijn veel manieren voor een aanvaller toodo dat, zoals door het hosten van een andere website die wordt geladen een resource van kwetsbare Hallo-server of ophalen Hallo gebruiker tooclick een koppeling.</span><span class="sxs-lookup"><span data-stu-id="83ebb-439">There are many ways for an attacker toodo that, such as by hosting a different web site that loads a resource from hello vulnerable server, or getting hello user tooclick a link.</span></span> <span data-ttu-id="83ebb-440">Hallo-aanval kan worden voorkomen als Hallo-server stuurt de client van een extra token toohello, vereist Hallo client tooinclude dat token in alle toekomstige aanvragen en verifieert dat alle toekomstige aanvragen een token dat betrekking heeft toohello huidige sessie bevatten, zoals door met behulp van ASP.NET AntiForgeryToken Hallo of ViewState.</span><span class="sxs-lookup"><span data-stu-id="83ebb-440">hello attack can be prevented if hello server sends an additional token toohello client, requires hello client tooinclude that token in all future requests, and verifies that all future requests include a token that pertains toohello current session, such as by using hello ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="83ebb-441">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-441">Title</span></span>                   | <span data-ttu-id="83ebb-442">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-443">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-443">**Component**</span></span>               | <span data-ttu-id="83ebb-444">Web-API</span><span class="sxs-lookup"><span data-stu-id="83ebb-444">Web API</span></span> | 
| <span data-ttu-id="83ebb-445">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-445">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-446">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-446">Build</span></span> |  
| <span data-ttu-id="83ebb-447">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-447">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="83ebb-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="83ebb-449">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-449">**Attributes**</span></span>              | <span data-ttu-id="83ebb-450">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="83ebb-450">N/A</span></span>  |
| <span data-ttu-id="83ebb-451">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-451">**References**</span></span>              | [<span data-ttu-id="83ebb-452">Het voorkomen van Aanvraagvervalsing op meerdere sites (CSRF) aanvallen in ASP.NET Web-API</span><span class="sxs-lookup"><span data-stu-id="83ebb-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="83ebb-453">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-453">**Steps**</span></span> | <span data-ttu-id="83ebb-454">Anti-CSRF en AJAX: Hallo formulier token kan een probleem voor AJAX-aanvragen worden, omdat een AJAX-aanvraag JSON-gegevens, geen HTML-formuliergegevens kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="83ebb-454">Anti-CSRF and AJAX: hello form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="83ebb-455">Eén oplossing is toosend Hallo tokens in een aangepaste HTTP-header.</span><span class="sxs-lookup"><span data-stu-id="83ebb-455">One solution is toosend hello tokens in a custom HTTP header.</span></span> <span data-ttu-id="83ebb-456">Hallo volgende code gebruikt Razor syntaxis toogenerate Hallo tokens en vervolgens voegt Hallo tokens tooan AJAX-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="83ebb-456">hello following code uses Razor syntax toogenerate hello tokens, and then adds hello tokens tooan AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="83ebb-457">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-457">Example</span></span>
```Javascript
<script>
    @functions{
        public string TokenHeaderValue()
        {
            string cookieToken, formToken;
            AntiForgery.GetTokens(null, out cookieToken, out formToken);
            return cookieToken + ":" + formToken;                
        }
    }
    $.ajax("api/values", {
        type: "post",
        contentType: "application/json",
        data: {  }, // JSON data goes here
        dataType: "json",
        headers: {
            'RequestVerificationToken': '@TokenHeaderValue()'
        }
    });
</script>
```

### <a name="example"></a><span data-ttu-id="83ebb-458">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-458">Example</span></span>
<span data-ttu-id="83ebb-459">Wanneer u Hallo aanvraag verwerkt, moet u Hallo tokens extraheren uit de aanvraagheader Hallo.</span><span class="sxs-lookup"><span data-stu-id="83ebb-459">When you process hello request, extract hello tokens from hello request header.</span></span> <span data-ttu-id="83ebb-460">Vervolgens roept Hallo AntiForgery.Validate methode toovalidate Hallo tokens.</span><span class="sxs-lookup"><span data-stu-id="83ebb-460">Then call hello AntiForgery.Validate method toovalidate hello tokens.</span></span> <span data-ttu-id="83ebb-461">Hallo methode Validate genereert een uitzondering als Hallo tokens niet geldig zijn.</span><span class="sxs-lookup"><span data-stu-id="83ebb-461">hello Validate method throws an exception if hello tokens are not valid.</span></span>
```C#
void ValidateRequestHeader(HttpRequestMessage request)
{
    string cookieToken = "";
    string formToken = "";

    IEnumerable<string> tokenHeaders;
    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
    {
        string[] tokens = tokenHeaders.First().Split(':');
        if (tokens.Length == 2)
        {
            cookieToken = tokens[0].Trim();
            formToken = tokens[1].Trim();
        }
    }
    AntiForgery.Validate(cookieToken, formToken);
}
```

### <a name="example"></a><span data-ttu-id="83ebb-462">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-462">Example</span></span>
<span data-ttu-id="83ebb-463">Anti-CSRF en formulieren in ASP.NET MVC - gebruik Hallo AntiForgeryToken Help-methode op weergaven; bijvoorbeeld, een Html.AntiForgeryToken() in Hallo formulier plaatsen</span><span class="sxs-lookup"><span data-stu-id="83ebb-463">Anti-CSRF and ASP.NET MVC forms - Use hello AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into hello form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="83ebb-464">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-464">Example</span></span>
<span data-ttu-id="83ebb-465">Hallo in bovenstaand voorbeeld wordt ongeveer de volgende Hallo uitvoer:</span><span class="sxs-lookup"><span data-stu-id="83ebb-465">hello example above will output something like hello following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="83ebb-466">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-466">Example</span></span>
<span data-ttu-id="83ebb-467">Op Hallo dezelfde tijdstip, Html.AntiForgeryToken() biedt Hallo bezoeker een cookie aangeroepen __RequestVerificationToken Hello dezelfde als Hallo willekeurige verborgen waarde waarde hierboven weergegeven.</span><span class="sxs-lookup"><span data-stu-id="83ebb-467">At hello same time, Html.AntiForgeryToken() gives hello visitor a cookie called __RequestVerificationToken, with hello same value as hello random hidden value shown above.</span></span> <span data-ttu-id="83ebb-468">Vervolgens voegt u toovalidate een binnenkomende Formulierbericht Hallo [ValidateAntiForgeryToken] filter toohello doel-actiemethode.</span><span class="sxs-lookup"><span data-stu-id="83ebb-468">Next, toovalidate an incoming form post, add hello [ValidateAntiForgeryToken] filter toohello target action method.</span></span> <span data-ttu-id="83ebb-469">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="83ebb-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="83ebb-470">Autorisatiefilter die of controleert:</span><span class="sxs-lookup"><span data-stu-id="83ebb-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="83ebb-471">Hallo binnenkomende aanvraag heeft een cookie met de naam __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="83ebb-471">hello incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="83ebb-472">Hallo binnenkomende aanvraag heeft een `Request.Form` vermelding __RequestVerificationToken aangeroepen</span><span class="sxs-lookup"><span data-stu-id="83ebb-472">hello incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="83ebb-473">Deze cookie en `Request.Form` waarden overeenkomen, ervan uitgaande dat alle goed is, doorloopt NTDS Hallo-aanvraag die normaal werken.</span><span class="sxs-lookup"><span data-stu-id="83ebb-473">These cookie and `Request.Form` values match Assuming all is well, hello request goes through as normal.</span></span> <span data-ttu-id="83ebb-474">Maar als dit niet het geval is, klikt u vervolgens een Autorisatiefout met het bericht 'een vereiste anti-vervalsingstoken is niet opgegeven of is ongeldig'.</span><span class="sxs-lookup"><span data-stu-id="83ebb-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="83ebb-475">Titel</span><span class="sxs-lookup"><span data-stu-id="83ebb-475">Title</span></span>                   | <span data-ttu-id="83ebb-476">Details</span><span class="sxs-lookup"><span data-stu-id="83ebb-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="83ebb-477">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="83ebb-477">**Component**</span></span>               | <span data-ttu-id="83ebb-478">Web-API</span><span class="sxs-lookup"><span data-stu-id="83ebb-478">Web API</span></span> | 
| <span data-ttu-id="83ebb-479">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="83ebb-479">**SDL Phase**</span></span>               | <span data-ttu-id="83ebb-480">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="83ebb-480">Build</span></span> |  
| <span data-ttu-id="83ebb-481">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="83ebb-481">**Applicable Technologies**</span></span> | <span data-ttu-id="83ebb-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="83ebb-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="83ebb-483">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="83ebb-483">**Attributes**</span></span>              | <span data-ttu-id="83ebb-484">ID-Provider - ADFS, identiteitsprovider - Azure AD</span><span class="sxs-lookup"><span data-stu-id="83ebb-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="83ebb-485">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-485">**References**</span></span>              | [<span data-ttu-id="83ebb-486">Een Web-API met afzonderlijke Accounts en lokale aanmelding in ASP.NET Web-API 2.2 beveiligen</span><span class="sxs-lookup"><span data-stu-id="83ebb-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="83ebb-487">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="83ebb-487">**Steps**</span></span> | <span data-ttu-id="83ebb-488">Als het Hallo-Web-API is beveiligd met OAuth 2.0, wordt verwacht bearer-token in autorisatie-aanvraag-header en verleent toegangsaanvraag toohello alleen als het Hallo-token is geldig.</span><span class="sxs-lookup"><span data-stu-id="83ebb-488">If hello Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access toohello request only if hello token is valid.</span></span> <span data-ttu-id="83ebb-489">In tegenstelling tot op basis van Cookieverificatie, worden Hallo bearer-tokens toorequests in browsers niet koppelen.</span><span class="sxs-lookup"><span data-stu-id="83ebb-489">Unlike cookie based authentication, browsers do not attach hello bearer tokens toorequests.</span></span> <span data-ttu-id="83ebb-490">Hallo vraagt de client moet tooexplicitly hello bearer-token in de aanvraagheader Hallo koppelen.</span><span class="sxs-lookup"><span data-stu-id="83ebb-490">hello requesting client needs tooexplicitly attach hello bearer token in hello request header.</span></span> <span data-ttu-id="83ebb-491">Daarom voor ASP.NET Web API's beveiligd met OAuth 2.0-bearer-tokens worden beschouwd als bij de bescherming tegen aanvallen CSRF.</span><span class="sxs-lookup"><span data-stu-id="83ebb-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="83ebb-492">Houd er rekening mee dat als Hallo MVC-gedeelte van de toepassing hello formulierverificatie (dat wil zeggen, maakt gebruik van cookies) gebruikt, ter voorkoming tokens toobe die wordt gebruikt door Hallo MVC-web-app hebt.</span><span class="sxs-lookup"><span data-stu-id="83ebb-492">Please note that if hello MVC portion of hello application uses forms authentication (i.e., uses cookies), anti-forgery tokens have toobe used by hello MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="83ebb-493">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="83ebb-493">Example</span></span>
<span data-ttu-id="83ebb-494">Hallo-Web-API heeft toobe op de hoogte toorely alleen op bearer-tokens en niet op cookies.</span><span class="sxs-lookup"><span data-stu-id="83ebb-494">hello Web API has toobe informed toorely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="83ebb-495">Het kan worden gedaan door de configuratie in de volgende Hallo `WebApiConfig.Register` methode: '''C-Sharp code config. SuppressDefaultHostAuthentication(); configuratie. Filters.Add (nieuwe HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="83ebb-495">It can be done by hello following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
hello SuppressDefaultHostAuthentication method tells Web API tooignore any authentication that happens before hello request reaches hello Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API tooauthenticate only using bearer tokens.

---
title: Sessie-Management - hulpmiddel voor het modelleren van Microsoft Threat - Azure | Microsoft Docs
description: oplossingen voor bedreigingen die worden weergegeven in het hulpprogramma Threat Modeling
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
ms.openlocfilehash: 56471d8ef68eacacb3ecebad5056d7e7a9f3ca40
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="security-frame-session-management--articles"></a><span data-ttu-id="316fd-103">Beveiliging Frame: Sessiebeheer | Artikelen</span><span class="sxs-lookup"><span data-stu-id="316fd-103">Security Frame: Session Management | Articles</span></span> 
| <span data-ttu-id="316fd-104">Product/Service</span><span class="sxs-lookup"><span data-stu-id="316fd-104">Product/Service</span></span> | <span data-ttu-id="316fd-105">Artikel</span><span class="sxs-lookup"><span data-stu-id="316fd-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="316fd-106">**Azure AD**</span><span class="sxs-lookup"><span data-stu-id="316fd-106">**Azure AD**</span></span>    | <ul><li>[<span data-ttu-id="316fd-107">De juiste afmelding implementeren met behulp van ADAL methoden bij gebruik van Azure AD</span><span class="sxs-lookup"><span data-stu-id="316fd-107">Implement proper logout using ADAL methods when using Azure AD</span></span>](#logout-adal)</li></ul> |
| <span data-ttu-id="316fd-108">IoT-apparaat</span><span class="sxs-lookup"><span data-stu-id="316fd-108">IoT Device</span></span> | <ul><li>[<span data-ttu-id="316fd-109">Het gebruiken van beperkte levensduur voor gegenereerde SaS-tokens</span><span class="sxs-lookup"><span data-stu-id="316fd-109">Use finite lifetimes for generated SaS tokens</span></span>](#finite-tokens)</li></ul> |
| <span data-ttu-id="316fd-110">**Azure Documentdb**</span><span class="sxs-lookup"><span data-stu-id="316fd-110">**Azure Document DB**</span></span> | <ul><li>[<span data-ttu-id="316fd-111">Minimale token levensduur voor tokens voor gegenereerde Resource gebruiken</span><span class="sxs-lookup"><span data-stu-id="316fd-111">Use minimum token lifetimes for generated Resource tokens</span></span>](#resource-tokens)</li></ul> |
| <span data-ttu-id="316fd-112">**ADFS**</span><span class="sxs-lookup"><span data-stu-id="316fd-112">**ADFS**</span></span> | <ul><li>[<span data-ttu-id="316fd-113">Juiste afmelding WsFederation methoden gebruiken wanneer u AD FS implementeren</span><span class="sxs-lookup"><span data-stu-id="316fd-113">Implement proper logout using WsFederation methods when using ADFS</span></span>](#wsfederation-logout)</li></ul> |
| <span data-ttu-id="316fd-114">**Identiteitsserver**</span><span class="sxs-lookup"><span data-stu-id="316fd-114">**Identity Server**</span></span> | <ul><li>[<span data-ttu-id="316fd-115">Implementeren in de juiste afmelden bij gebruik van Identiteitsserver</span><span class="sxs-lookup"><span data-stu-id="316fd-115">Implement proper logout when using Identity Server</span></span>](#proper-logout)</li></ul> |
| <span data-ttu-id="316fd-116">**Webtoepassing**</span><span class="sxs-lookup"><span data-stu-id="316fd-116">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="316fd-117">Toepassingen die beschikbaar zijn via HTTPS moeten beveiligde cookies gebruiken</span><span class="sxs-lookup"><span data-stu-id="316fd-117">Applications available over HTTPS must use secure cookies</span></span>](#https-secure-cookies)</li><li>[<span data-ttu-id="316fd-118">Alle HTTP-gebaseerde toepassing moet http alleen voor de definitie van de cookie opgeven</span><span class="sxs-lookup"><span data-stu-id="316fd-118">All http based application should specify http only for cookie definition</span></span>](#cookie-definition)</li><li>[<span data-ttu-id="316fd-119">Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET-webpagina 's</span><span class="sxs-lookup"><span data-stu-id="316fd-119">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>](#csrf-asp)</li><li>[<span data-ttu-id="316fd-120">Sessie voor inactiviteit levensduur instellen</span><span class="sxs-lookup"><span data-stu-id="316fd-120">Set up session for inactivity lifetime</span></span>](#inactivity-lifetime)</li><li>[<span data-ttu-id="316fd-121">Juiste afmelden van de toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="316fd-121">Implement proper logout from the application</span></span>](#proper-app-logout)</li></ul> |
| <span data-ttu-id="316fd-122">**Web-API**</span><span class="sxs-lookup"><span data-stu-id="316fd-122">**Web API**</span></span> | <ul><li>[<span data-ttu-id="316fd-123">Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET Web-API 's</span><span class="sxs-lookup"><span data-stu-id="316fd-123">Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>](#csrf-api)</li></ul> |

## <span data-ttu-id="316fd-124"><a id="logout-adal"></a>De juiste afmelding implementeren met behulp van ADAL methoden bij gebruik van Azure AD</span><span class="sxs-lookup"><span data-stu-id="316fd-124"><a id="logout-adal"></a>Implement proper logout using ADAL methods when using Azure AD</span></span>

| <span data-ttu-id="316fd-125">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-125">Title</span></span>                   | <span data-ttu-id="316fd-126">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-126">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-127">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-127">**Component**</span></span>               | <span data-ttu-id="316fd-128">Azure AD</span><span class="sxs-lookup"><span data-stu-id="316fd-128">Azure AD</span></span> | 
| <span data-ttu-id="316fd-129">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-129">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-130">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-130">Build</span></span> |  
| <span data-ttu-id="316fd-131">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-131">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-132">Algemene</span><span class="sxs-lookup"><span data-stu-id="316fd-132">Generic</span></span> |
| <span data-ttu-id="316fd-133">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-133">**Attributes**</span></span>              | <span data-ttu-id="316fd-134">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-134">N/A</span></span>  |
| <span data-ttu-id="316fd-135">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-135">**References**</span></span>              | <span data-ttu-id="316fd-136">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-136">N/A</span></span>  |
| <span data-ttu-id="316fd-137">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-137">**Steps**</span></span> | <span data-ttu-id="316fd-138">Als de toepassing op access token dat is uitgegeven door Azure AD vertrouwt, moet de afmelding gebeurtenis-handler aanroepen</span><span class="sxs-lookup"><span data-stu-id="316fd-138">If the application relies on access token issued by Azure AD, the logout event handler should call</span></span> |

### <a name="example"></a><span data-ttu-id="316fd-139">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-139">Example</span></span>
```C#
HttpContext.GetOwinContext().Authentication.SignOut(OpenIdConnectAuthenticationDefaults.AuthenticationType, CookieAuthenticationDefaults.AuthenticationType)
```

### <a name="example"></a><span data-ttu-id="316fd-140">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-140">Example</span></span>
<span data-ttu-id="316fd-141">Het moet ook de gebruikerssessie door het aanroepen van methode Session.Abandon() vernietigen.</span><span class="sxs-lookup"><span data-stu-id="316fd-141">It should also destroy user's session by calling Session.Abandon() method.</span></span> <span data-ttu-id="316fd-142">Methode, ziet u beveiligde implementatie van de gebruiker afmelden in:</span><span class="sxs-lookup"><span data-stu-id="316fd-142">Following method shows secure implementation of user logout:</span></span>
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

## <span data-ttu-id="316fd-143"><a id="finite-tokens"></a>Het gebruiken van beperkte levensduur voor gegenereerde SaS-tokens</span><span class="sxs-lookup"><span data-stu-id="316fd-143"><a id="finite-tokens"></a>Use finite lifetimes for generated SaS tokens</span></span>

| <span data-ttu-id="316fd-144">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-144">Title</span></span>                   | <span data-ttu-id="316fd-145">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-145">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-146">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-146">**Component**</span></span>               | <span data-ttu-id="316fd-147">IoT-apparaat</span><span class="sxs-lookup"><span data-stu-id="316fd-147">IoT Device</span></span> | 
| <span data-ttu-id="316fd-148">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-148">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-149">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-149">Build</span></span> |  
| <span data-ttu-id="316fd-150">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-150">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-151">Algemene</span><span class="sxs-lookup"><span data-stu-id="316fd-151">Generic</span></span> |
| <span data-ttu-id="316fd-152">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-152">**Attributes**</span></span>              | <span data-ttu-id="316fd-153">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-153">N/A</span></span>  |
| <span data-ttu-id="316fd-154">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-154">**References**</span></span>              | <span data-ttu-id="316fd-155">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-155">N/A</span></span>  |
| <span data-ttu-id="316fd-156">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-156">**Steps**</span></span> | <span data-ttu-id="316fd-157">SaS-tokens gegenereerd voor verificatie bij de Azure IoT Hub moeten een eindige verloopperiode hebben.</span><span class="sxs-lookup"><span data-stu-id="316fd-157">SaS tokens generated for authenticating to Azure IoT Hub should have a finite expiry period.</span></span> <span data-ttu-id="316fd-158">Houd de levensduur van SaS-token tot een minimum te beperken van de hoeveelheid tijd die kunnen worden cookies voor het geval de tokens worden getroffen.</span><span class="sxs-lookup"><span data-stu-id="316fd-158">Keep the SaS token lifetimes to a minimum to limit the amount of time they can be replayed in case the tokens are compromised.</span></span>|

## <span data-ttu-id="316fd-159"><a id="resource-tokens"></a>Minimale token levensduur voor tokens voor gegenereerde Resource gebruiken</span><span class="sxs-lookup"><span data-stu-id="316fd-159"><a id="resource-tokens"></a>Use minimum token lifetimes for generated Resource tokens</span></span>

| <span data-ttu-id="316fd-160">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-160">Title</span></span>                   | <span data-ttu-id="316fd-161">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-162">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-162">**Component**</span></span>               | <span data-ttu-id="316fd-163">Azure Documentdb</span><span class="sxs-lookup"><span data-stu-id="316fd-163">Azure Document DB</span></span> | 
| <span data-ttu-id="316fd-164">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-164">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-165">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-165">Build</span></span> |  
| <span data-ttu-id="316fd-166">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-166">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-167">Algemene</span><span class="sxs-lookup"><span data-stu-id="316fd-167">Generic</span></span> |
| <span data-ttu-id="316fd-168">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-168">**Attributes**</span></span>              | <span data-ttu-id="316fd-169">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-169">N/A</span></span>  |
| <span data-ttu-id="316fd-170">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-170">**References**</span></span>              | <span data-ttu-id="316fd-171">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-171">N/A</span></span>  |
| <span data-ttu-id="316fd-172">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-172">**Steps**</span></span> | <span data-ttu-id="316fd-173">Het interval van resource token beperken tot een voorgeschreven minimumwaarde.</span><span class="sxs-lookup"><span data-stu-id="316fd-173">Reduce the timespan of resource token to a minimum value required.</span></span> <span data-ttu-id="316fd-174">Resource-tokens hebben een geldige timespan standaardwaarde van 1 uur.</span><span class="sxs-lookup"><span data-stu-id="316fd-174">Resource tokens have a default valid timespan of 1 hour.</span></span>|

## <span data-ttu-id="316fd-175"><a id="wsfederation-logout"></a>Juiste afmelding WsFederation methoden gebruiken wanneer u AD FS implementeren</span><span class="sxs-lookup"><span data-stu-id="316fd-175"><a id="wsfederation-logout"></a>Implement proper logout using WsFederation methods when using ADFS</span></span>

| <span data-ttu-id="316fd-176">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-176">Title</span></span>                   | <span data-ttu-id="316fd-177">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-177">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-178">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-178">**Component**</span></span>               | <span data-ttu-id="316fd-179">ADFS</span><span class="sxs-lookup"><span data-stu-id="316fd-179">ADFS</span></span> | 
| <span data-ttu-id="316fd-180">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-180">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-181">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-181">Build</span></span> |  
| <span data-ttu-id="316fd-182">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-182">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-183">Algemene</span><span class="sxs-lookup"><span data-stu-id="316fd-183">Generic</span></span> |
| <span data-ttu-id="316fd-184">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-184">**Attributes**</span></span>              | <span data-ttu-id="316fd-185">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-185">N/A</span></span>  |
| <span data-ttu-id="316fd-186">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-186">**References**</span></span>              | <span data-ttu-id="316fd-187">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-187">N/A</span></span>  |
| <span data-ttu-id="316fd-188">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-188">**Steps**</span></span> | <span data-ttu-id="316fd-189">Als de toepassing afhankelijk is uitgegeven door AD FS STS-token, moet de gebeurtenis-handler voor afmelden WSFederationAuthenticationModule.FederatedSignOut() methode afmelden van de gebruiker aanroepen.</span><span class="sxs-lookup"><span data-stu-id="316fd-189">If the application relies on STS token issued by ADFS, the logout event handler should call WSFederationAuthenticationModule.FederatedSignOut() method to log out the user.</span></span> <span data-ttu-id="316fd-190">Ook de huidige sessie moet worden vernietigd en de waarde voor de sessie-token te herstellen en geneutraliseerd.</span><span class="sxs-lookup"><span data-stu-id="316fd-190">Also the current session should be destroyed, and the session token value should be reset and nullified.</span></span>|

### <a name="example"></a><span data-ttu-id="316fd-191">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-191">Example</span></span>
```C#
        [HttpPost, ValidateAntiForgeryToken]
        [Authorization]
        public ActionResult SignOut(string redirectUrl)
        {
            if (!this.User.Identity.IsAuthenticated)
            {
                return this.View("LogOff", null);
            }

            // Removes the user profile.
            this.Session.Clear();
            this.Session.Abandon();
            HttpContext.Current.Response.Cookies.Add(new System.Web.HttpCookie("ASP.NET_SessionId", string.Empty)
                {
                    Expires = DateTime.Now.AddDays(-1D),
                    Secure = true,
                    HttpOnly = true
                });

            // Signs out at the specified security token service (STS) by using the WS-Federation protocol.
            Uri signOutUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Issuer);
            Uri replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm);
            if (!string.IsNullOrEmpty(redirectUrl))
            {
                replyUrl = new Uri(FederatedAuthentication.WSFederationAuthenticationModule.Realm + redirectUrl);
            }
           //     Signs out of the current session and raises the appropriate events.
            var authModule = FederatedAuthentication.WSFederationAuthenticationModule;
            authModule.SignOut(false);
        //     Signs out at the specified security token service (STS) by using the WS-Federation
        //     protocol.            
            WSFederationAuthenticationModule.FederatedSignOut(signOutUrl, replyUrl);
            return new RedirectResult(redirectUrl);
        }
```

## <span data-ttu-id="316fd-192"><a id="proper-logout"></a>Implementeren in de juiste afmelden bij gebruik van Identiteitsserver</span><span class="sxs-lookup"><span data-stu-id="316fd-192"><a id="proper-logout"></a>Implement proper logout when using Identity Server</span></span>

| <span data-ttu-id="316fd-193">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-193">Title</span></span>                   | <span data-ttu-id="316fd-194">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-194">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-195">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-195">**Component**</span></span>               | <span data-ttu-id="316fd-196">Identiteitsserver</span><span class="sxs-lookup"><span data-stu-id="316fd-196">Identity Server</span></span> | 
| <span data-ttu-id="316fd-197">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-197">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-198">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-198">Build</span></span> |  
| <span data-ttu-id="316fd-199">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-199">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-200">Algemene</span><span class="sxs-lookup"><span data-stu-id="316fd-200">Generic</span></span> |
| <span data-ttu-id="316fd-201">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-201">**Attributes**</span></span>              | <span data-ttu-id="316fd-202">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-202">N/A</span></span>  |
| <span data-ttu-id="316fd-203">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-203">**References**</span></span>              | [<span data-ttu-id="316fd-204">IdentityServer3 federatieve afmelden</span><span class="sxs-lookup"><span data-stu-id="316fd-204">IdentityServer3-Federated sign out</span></span>](https://identityserver.github.io/Documentation/docsv2/advanced/federated-signout.html) |
| <span data-ttu-id="316fd-205">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-205">**Steps**</span></span> | <span data-ttu-id="316fd-206">IdentityServer ondersteunt de mogelijkheid om te communiceren met externe id-providers.</span><span class="sxs-lookup"><span data-stu-id="316fd-206">IdentityServer supports the ability to federate with external identity providers.</span></span> <span data-ttu-id="316fd-207">Wanneer een gebruiker zich afmeldt een upstream-id-provider, is afhankelijk van het protocol dat wordt gebruikt, het mogelijk een melding te ontvangen wanneer de gebruiker zich afmeldt. Kunt u IdentityServer ervan om clients te verwittigen zodat ze kunnen ook de gebruiker zich af. Raadpleeg de documentatie in de sectie Verwijzingen voor details over de implementatie.</span><span class="sxs-lookup"><span data-stu-id="316fd-207">When a user signs out of an upstream identity provider, depending upon the protocol used, it might be possible to receive a notification when the user signs out. It allows IdentityServer to notify its clients so they can also sign the user out. Check the documentation in the references section for the implementation details.</span></span>|

## <span data-ttu-id="316fd-208"><a id="https-secure-cookies"></a>Toepassingen die beschikbaar zijn via HTTPS moeten beveiligde cookies gebruiken</span><span class="sxs-lookup"><span data-stu-id="316fd-208"><a id="https-secure-cookies"></a>Applications available over HTTPS must use secure cookies</span></span>

| <span data-ttu-id="316fd-209">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-209">Title</span></span>                   | <span data-ttu-id="316fd-210">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-210">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-211">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-211">**Component**</span></span>               | <span data-ttu-id="316fd-212">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="316fd-212">Web Application</span></span> | 
| <span data-ttu-id="316fd-213">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-213">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-214">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-214">Build</span></span> |  
| <span data-ttu-id="316fd-215">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-215">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-216">Algemene</span><span class="sxs-lookup"><span data-stu-id="316fd-216">Generic</span></span> |
| <span data-ttu-id="316fd-217">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-217">**Attributes**</span></span>              | <span data-ttu-id="316fd-218">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="316fd-218">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="316fd-219">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-219">**References**</span></span>              | <span data-ttu-id="316fd-220">[httpCookies Element (ASP.NET-instellingenschema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure-eigenschap](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span><span class="sxs-lookup"><span data-stu-id="316fd-220">[httpCookies Element (ASP.NET Settings Schema)](http://msdn.microsoft.com/library/ms228262(v=vs.100).aspx), [HttpCookie.Secure Property](http://msdn.microsoft.com/library/system.web.httpcookie.secure.aspx)</span></span> |
| <span data-ttu-id="316fd-221">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-221">**Steps**</span></span> | <span data-ttu-id="316fd-222">Cookies zijn normaal gesproken alleen toegankelijk is voor het domein waarvoor ze zijn binnen het bereik.</span><span class="sxs-lookup"><span data-stu-id="316fd-222">Cookies are normally only accessible to the domain for which they were scoped.</span></span> <span data-ttu-id="316fd-223">Helaas bevat de definitie van 'domein' geen het protocol zodat cookies die zijn gemaakt via HTTPS toegankelijk via HTTP zijn.</span><span class="sxs-lookup"><span data-stu-id="316fd-223">Unfortunately, the definition of "domain" does not include the protocol so cookies that are created over HTTPS are accessible over HTTP.</span></span> <span data-ttu-id="316fd-224">Het kenmerk 'secure' geeft u aan de browser dat de cookie alleen beschikbaar moet worden gesteld via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="316fd-224">The "secure" attribute indicates to the browser that the cookie should only be made available over HTTPS.</span></span> <span data-ttu-id="316fd-225">Zorg ervoor dat alle cookies moet worden ingesteld via HTTPS gebruikt de **beveiligde** kenmerk.</span><span class="sxs-lookup"><span data-stu-id="316fd-225">Ensure that all cookies set over HTTPS use the **secure** attribute.</span></span> <span data-ttu-id="316fd-226">Aan deze eis kan worden afgedwongen in het web.config-bestand door het kenmerk requireSSL in te stellen op true.</span><span class="sxs-lookup"><span data-stu-id="316fd-226">The requirement can be enforced in the web.config file by setting the requireSSL attribute to true.</span></span> <span data-ttu-id="316fd-227">De gewenste aanpak omdat deze wordt afgedwongen wordt de **beveiligde** kenmerk voor alle huidige en toekomstige cookies zonder aanvullende codewijzigingen aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="316fd-227">It is the preferred approach because it will enforce the **secure** attribute for all current and future cookies without the need to make any additional code changes.</span></span>|

### <a name="example"></a><span data-ttu-id="316fd-228">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-228">Example</span></span>
```C#
<configuration>
  <system.web>
    <httpCookies requireSSL="true"/>
  </system.web>
</configuration>
```
<span data-ttu-id="316fd-229">De instelling wordt afgedwongen, zelfs als HTTP is gebruikt voor toegang tot de toepassing.</span><span class="sxs-lookup"><span data-stu-id="316fd-229">The setting is enforced even if HTTP is used to access the application.</span></span> <span data-ttu-id="316fd-230">HTTP wordt gebruikt om toegang tot de toepassing, verbroken de instelling als de toepassing omdat de cookies worden ingesteld met het kenmerk secure en de browser ze niet terug naar de toepassing stuurt.</span><span class="sxs-lookup"><span data-stu-id="316fd-230">If HTTP is used to access the application, the setting breaks the application because the cookies are set with the secure attribute and the browser will not send them back to the application.</span></span>

| <span data-ttu-id="316fd-231">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-231">Title</span></span>                   | <span data-ttu-id="316fd-232">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-232">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-233">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-233">**Component**</span></span>               | <span data-ttu-id="316fd-234">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="316fd-234">Web Application</span></span> | 
| <span data-ttu-id="316fd-235">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-235">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-236">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-236">Build</span></span> |  
| <span data-ttu-id="316fd-237">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-237">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-238">Webformulieren, MVC5</span><span class="sxs-lookup"><span data-stu-id="316fd-238">Web Forms, MVC5</span></span> |
| <span data-ttu-id="316fd-239">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-239">**Attributes**</span></span>              | <span data-ttu-id="316fd-240">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="316fd-240">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="316fd-241">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-241">**References**</span></span>              | <span data-ttu-id="316fd-242">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-242">N/A</span></span>  |
| <span data-ttu-id="316fd-243">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-243">**Steps**</span></span> | <span data-ttu-id="316fd-244">Wanneer de webtoepassing de Relying Party is en de IdP ADFS-server, beveiligde kenmerk van het FedAuth-token kan worden geconfigureerd door requireSSL in te stellen op True in `system.identityModel.services` sectie van web.config:</span><span class="sxs-lookup"><span data-stu-id="316fd-244">When the web application is the Relying Party, and the IdP is ADFS server, the FedAuth token's secure attribute can be configured by setting requireSSL to True in `system.identityModel.services` section of web.config:</span></span>|

### <a name="example"></a><span data-ttu-id="316fd-245">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-245">Example</span></span>
```C#
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:20:0" />
    ....  
    </federationConfiguration>
  </system.identityModel.services>
```

## <span data-ttu-id="316fd-246"><a id="cookie-definition"></a>Alle HTTP-gebaseerde toepassing moet http alleen voor de definitie van de cookie opgeven</span><span class="sxs-lookup"><span data-stu-id="316fd-246"><a id="cookie-definition"></a>All http based application should specify http only for cookie definition</span></span>

| <span data-ttu-id="316fd-247">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-247">Title</span></span>                   | <span data-ttu-id="316fd-248">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-248">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-249">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-249">**Component**</span></span>               | <span data-ttu-id="316fd-250">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="316fd-250">Web Application</span></span> | 
| <span data-ttu-id="316fd-251">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-251">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-252">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-252">Build</span></span> |  
| <span data-ttu-id="316fd-253">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-253">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-254">Algemene</span><span class="sxs-lookup"><span data-stu-id="316fd-254">Generic</span></span> |
| <span data-ttu-id="316fd-255">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-255">**Attributes**</span></span>              | <span data-ttu-id="316fd-256">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-256">N/A</span></span>  |
| <span data-ttu-id="316fd-257">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-257">**References**</span></span>              | [<span data-ttu-id="316fd-258">Beveiligde Cookie-kenmerk</span><span class="sxs-lookup"><span data-stu-id="316fd-258">Secure Cookie Attribute</span></span>](https://en.wikipedia.org/wiki/HTTP_cookie#Secure_cookie) |
| <span data-ttu-id="316fd-259">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-259">**Steps**</span></span> | <span data-ttu-id="316fd-260">Zodat het risico van de openbaarmaking van informatie met een aanval cross-site scripting (XSS) van een nieuw kenmerk - httpOnly - om cookies te werd geïntroduceerd en wordt ondersteund door alle belangrijke browsers.</span><span class="sxs-lookup"><span data-stu-id="316fd-260">To mitigate the risk of information disclosure with a cross-site scripting (XSS) attack, a new attribute - httpOnly - was introduced to cookies and is supported by all major browsers.</span></span> <span data-ttu-id="316fd-261">Het kenmerk geeft u een cookie is niet toegankelijk via script.</span><span class="sxs-lookup"><span data-stu-id="316fd-261">The attribute specifies that a cookie is not accessible through script.</span></span> <span data-ttu-id="316fd-262">Met behulp van cookies HttpOnly verkleint een webtoepassing de kans dat gevoelige informatie in de cookie kan worden gestolen via scripts en naar de website van een aanvaller verzonden.</span><span class="sxs-lookup"><span data-stu-id="316fd-262">By using HttpOnly cookies, a web application reduces the possibility that sensitive information contained in the cookie can be stolen via script and sent to an attacker's website.</span></span> |

### <a name="example"></a><span data-ttu-id="316fd-263">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-263">Example</span></span>
<span data-ttu-id="316fd-264">Alle HTTP-gebaseerde toepassingen die gebruikmaken van cookies moeten in de definitie van het cookie door het implementeren van na de configuratie in web.config HttpOnly opgeven:</span><span class="sxs-lookup"><span data-stu-id="316fd-264">All HTTP-based applications that use cookies should specify HttpOnly in the cookie definition, by implementing following configuration in web.config:</span></span>
```XML
<system.web>
.
.
   <httpCookies requireSSL="false" httpOnlyCookies="true"/>
.
.
</system.web>
```

| <span data-ttu-id="316fd-265">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-265">Title</span></span>                   | <span data-ttu-id="316fd-266">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-266">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-267">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-267">**Component**</span></span>               | <span data-ttu-id="316fd-268">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="316fd-268">Web Application</span></span> | 
| <span data-ttu-id="316fd-269">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-269">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-270">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-270">Build</span></span> |  
| <span data-ttu-id="316fd-271">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-271">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-272">Web Forms</span><span class="sxs-lookup"><span data-stu-id="316fd-272">Web Forms</span></span> |
| <span data-ttu-id="316fd-273">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-273">**Attributes**</span></span>              | <span data-ttu-id="316fd-274">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-274">N/A</span></span>  |
| <span data-ttu-id="316fd-275">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-275">**References**</span></span>              | [<span data-ttu-id="316fd-276">De eigenschap FormsAuthentication.RequireSSL</span><span class="sxs-lookup"><span data-stu-id="316fd-276">FormsAuthentication.RequireSSL Property</span></span>](https://msdn.microsoft.com/library/system.web.security.formsauthentication.requiressl.aspx) |
| <span data-ttu-id="316fd-277">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-277">**Steps**</span></span> | <span data-ttu-id="316fd-278">De waarde van de eigenschap RequireSSL is ingesteld in het configuratiebestand voor een ASP.NET-toepassing met behulp van het kenmerk requireSSL van het configuratie-element.</span><span class="sxs-lookup"><span data-stu-id="316fd-278">The RequireSSL property value is set in the configuration file for an ASP.NET application by using the requireSSL attribute of the configuration element.</span></span> <span data-ttu-id="316fd-279">U kunt opgeven in het bestand Web.config voor uw ASP.NET-toepassing of SSL (Secure Sockets Layer) vereist is voor de cookie voor formulierverificatie terugkeren naar de server door het kenmerk requireSSL.</span><span class="sxs-lookup"><span data-stu-id="316fd-279">You can specify in the Web.config file for your ASP.NET application whether SSL (Secure Sockets Layer) is required to return the forms-authentication cookie to the server by setting the requireSSL attribute.</span></span>|

### <a name="example"></a><span data-ttu-id="316fd-280">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-280">Example</span></span> 
<span data-ttu-id="316fd-281">Het volgende codevoorbeeld stelt het kenmerk requireSSL in het bestand Web.config.</span><span class="sxs-lookup"><span data-stu-id="316fd-281">The following code example sets the requireSSL attribute in the Web.config file.</span></span>
```XML
<authentication mode="Forms">
  <forms loginUrl="member_login.aspx" cookieless="UseCookies" requireSSL="true"/>
</authentication>
```

| <span data-ttu-id="316fd-282">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-282">Title</span></span>                   | <span data-ttu-id="316fd-283">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-283">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-284">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-284">**Component**</span></span>               | <span data-ttu-id="316fd-285">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="316fd-285">Web Application</span></span> | 
| <span data-ttu-id="316fd-286">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-286">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-287">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-287">Build</span></span> |  
| <span data-ttu-id="316fd-288">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-288">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-289">MVC5</span><span class="sxs-lookup"><span data-stu-id="316fd-289">MVC5</span></span> |
| <span data-ttu-id="316fd-290">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-290">**Attributes**</span></span>              | <span data-ttu-id="316fd-291">EnvironmentType - OnPrem</span><span class="sxs-lookup"><span data-stu-id="316fd-291">EnvironmentType - OnPrem</span></span> |
| <span data-ttu-id="316fd-292">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-292">**References**</span></span>              | [<span data-ttu-id="316fd-293">Configuratie van Windows Identity Foundation (WIF) – deel II</span><span class="sxs-lookup"><span data-stu-id="316fd-293">Windows Identity Foundation (WIF) Configuration – Part II</span></span>](https://blogs.msdn.microsoft.com/alikl/2011/02/01/windows-identity-foundation-wif-configuration-part-ii-cookiehandler-chunkedcookiehandler-customcookiehandler/) |
| <span data-ttu-id="316fd-294">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-294">**Steps**</span></span> | <span data-ttu-id="316fd-295">Om in te stellen kenmerk httpOnly voor FedAuth cookies, moet de kenmerkwaarde hideFromCsript worden ingesteld op True.</span><span class="sxs-lookup"><span data-stu-id="316fd-295">To set httpOnly attribute for FedAuth cookies, hideFromCsript attribute value should be set to True.</span></span> |

### <a name="example"></a><span data-ttu-id="316fd-296">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-296">Example</span></span>
<span data-ttu-id="316fd-297">Volgende configuratie ziet u de juiste configuratie:</span><span class="sxs-lookup"><span data-stu-id="316fd-297">Following configuration shows the correct configuration:</span></span>
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

## <span data-ttu-id="316fd-298"><a id="csrf-asp"></a>Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET-webpagina 's</span><span class="sxs-lookup"><span data-stu-id="316fd-298"><a id="csrf-asp"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET web pages</span></span>

| <span data-ttu-id="316fd-299">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-299">Title</span></span>                   | <span data-ttu-id="316fd-300">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-300">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-301">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-301">**Component**</span></span>               | <span data-ttu-id="316fd-302">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="316fd-302">Web Application</span></span> | 
| <span data-ttu-id="316fd-303">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-303">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-304">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-304">Build</span></span> |  
| <span data-ttu-id="316fd-305">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-305">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-306">Algemene</span><span class="sxs-lookup"><span data-stu-id="316fd-306">Generic</span></span> |
| <span data-ttu-id="316fd-307">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-307">**Attributes**</span></span>              | <span data-ttu-id="316fd-308">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-308">N/A</span></span>  |
| <span data-ttu-id="316fd-309">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-309">**References**</span></span>              | <span data-ttu-id="316fd-310">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-310">N/A</span></span>  |
| <span data-ttu-id="316fd-311">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-311">**Steps**</span></span> | <span data-ttu-id="316fd-312">Aanvraagvervalsing op meerdere sites (CSRF of XSRF) is een type van een aanval waarbij een aanvaller acties in de beveiligingscontext van de vastgestelde sessie een andere gebruiker op een website kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="316fd-312">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="316fd-313">Het doel is om te wijzigen of verwijderen van inhoud, als voor de betreffende website uitsluitend sessiecookies ontvangen request verifiëren.</span><span class="sxs-lookup"><span data-stu-id="316fd-313">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="316fd-314">Een aanvaller kan deze kwetsbaarheid misbruiken met het ophalen van de browser een URL met een opdracht laden van een kwetsbaar site waarop de gebruiker is aangemeld in een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="316fd-314">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="316fd-315">Er zijn veel manieren voor aanvallers om u te doen, zoals door die als host fungeert voor een andere website die wordt een resource van de server kwetsbaar wordt geladen, of voor het verkrijgen van de gebruiker op een koppeling te klikken.</span><span class="sxs-lookup"><span data-stu-id="316fd-315">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="316fd-316">De aanval kan worden voorkomen als de server een extra token naar de client verzendt vereist dat de client die token opnemen in alle toekomstige aanvragen en verifieert dat alle toekomstige aanvragen een token dat betrekking op de huidige sessie bevatten, heeft zoals met behulp van de ASP.NET AntiForgeryToken of ViewState.</span><span class="sxs-lookup"><span data-stu-id="316fd-316">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="316fd-317">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-317">Title</span></span>                   | <span data-ttu-id="316fd-318">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-318">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-319">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-319">**Component**</span></span>               | <span data-ttu-id="316fd-320">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="316fd-320">Web Application</span></span> | 
| <span data-ttu-id="316fd-321">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-321">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-322">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-322">Build</span></span> |  
| <span data-ttu-id="316fd-323">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-323">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-324">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="316fd-324">MVC5, MVC6</span></span> |
| <span data-ttu-id="316fd-325">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-325">**Attributes**</span></span>              | <span data-ttu-id="316fd-326">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-326">N/A</span></span>  |
| <span data-ttu-id="316fd-327">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-327">**References**</span></span>              | [<span data-ttu-id="316fd-328">XSRF/CSRF voorkomen in ASP.NET MVC en webpagina 's</span><span class="sxs-lookup"><span data-stu-id="316fd-328">XSRF/CSRF Prevention in ASP.NET MVC and Web Pages</span></span>](http://www.asp.net/mvc/overview/security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages) |
| <span data-ttu-id="316fd-329">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-329">**Steps**</span></span> | <span data-ttu-id="316fd-330">Anti-CSRF en formulieren ASP.NET MVC - gebruiken de `AntiForgeryToken` Help-methode op weergaven; put een `Html.AntiForgeryToken()` in het formulier, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="316fd-330">Anti-CSRF and ASP.NET MVC forms - Use the `AntiForgeryToken` helper method on Views; put an `Html.AntiForgeryToken()` into the form, for example,</span></span>|

### <a name="example"></a><span data-ttu-id="316fd-331">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-331">Example</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
```

### <a name="example"></a><span data-ttu-id="316fd-332">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-332">Example</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="316fd-333">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-333">Example</span></span>
<span data-ttu-id="316fd-334">Op hetzelfde moment biedt Html.AntiForgeryToken() de bezoeker een cookie met de naam __RequestVerificationToken met dezelfde waarde als de willekeurige verborgen waarde hierboven weergegeven.</span><span class="sxs-lookup"><span data-stu-id="316fd-334">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="316fd-335">Vervolgens voegt u het filter [ValidateAntiForgeryToken] aan doelmethode actie voor het valideren van een binnenkomende Formulierbericht.</span><span class="sxs-lookup"><span data-stu-id="316fd-335">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="316fd-336">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="316fd-336">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="316fd-337">Autorisatiefilter die of controleert:</span><span class="sxs-lookup"><span data-stu-id="316fd-337">Authorization filter that checks that:</span></span>
* <span data-ttu-id="316fd-338">De binnenkomende aanvraag heeft een cookie met de naam __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="316fd-338">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="316fd-339">De binnenkomende aanvraag heeft een `Request.Form` vermelding __RequestVerificationToken aangeroepen</span><span class="sxs-lookup"><span data-stu-id="316fd-339">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="316fd-340">Deze cookie en `Request.Form` waarden overeenkomen, ervan uitgaande dat alle goed is, de aanvraag wordt verwerkt via die normaal werken.</span><span class="sxs-lookup"><span data-stu-id="316fd-340">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="316fd-341">Maar als dit niet het geval is, klikt u vervolgens een Autorisatiefout met het bericht 'een vereiste anti-vervalsingstoken is niet opgegeven of is ongeldig'.</span><span class="sxs-lookup"><span data-stu-id="316fd-341">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span> 

### <a name="example"></a><span data-ttu-id="316fd-342">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-342">Example</span></span>
<span data-ttu-id="316fd-343">Anti-CSRF en AJAX: het token van het formulier een probleem voor AJAX-aanvragen kan worden, omdat een AJAX-aanvraag JSON-gegevens, geen HTML-formuliergegevens kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="316fd-343">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="316fd-344">Eén oplossing is voor het verzenden van de tokens in een aangepaste HTTP-header.</span><span class="sxs-lookup"><span data-stu-id="316fd-344">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="316fd-345">De volgende code Razor syntaxis wordt gebruikt voor het genereren van de tokens en vervolgens de tokens toegevoegd aan een AJAX-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="316fd-345">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> 
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

### <a name="example"></a><span data-ttu-id="316fd-346">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-346">Example</span></span>
<span data-ttu-id="316fd-347">Wanneer u de aanvraag verwerkt, moet u de tokens extraheren uit de aanvraagheader.</span><span class="sxs-lookup"><span data-stu-id="316fd-347">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="316fd-348">Vervolgens roept de methode AntiForgery.Validate voor het valideren van de tokens.</span><span class="sxs-lookup"><span data-stu-id="316fd-348">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="316fd-349">De methode Validate genereert een uitzondering als de tokens niet geldig zijn.</span><span class="sxs-lookup"><span data-stu-id="316fd-349">The Validate method throws an exception if the tokens are not valid.</span></span>
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

| <span data-ttu-id="316fd-350">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-350">Title</span></span>                   | <span data-ttu-id="316fd-351">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-351">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-352">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-352">**Component**</span></span>               | <span data-ttu-id="316fd-353">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="316fd-353">Web Application</span></span> | 
| <span data-ttu-id="316fd-354">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-354">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-355">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-355">Build</span></span> |  
| <span data-ttu-id="316fd-356">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-356">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-357">Web Forms</span><span class="sxs-lookup"><span data-stu-id="316fd-357">Web Forms</span></span> |
| <span data-ttu-id="316fd-358">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-358">**Attributes**</span></span>              | <span data-ttu-id="316fd-359">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-359">N/A</span></span>  |
| <span data-ttu-id="316fd-360">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-360">**References**</span></span>              | [<span data-ttu-id="316fd-361">Profiteren van ASP.NET ingebouwde functies voor Fend uit aanvallen via Internet</span><span class="sxs-lookup"><span data-stu-id="316fd-361">Take Advantage of ASP.NET Built-in Features to Fend Off Web Attacks</span></span>](https://msdn.microsoft.com/library/ms972969.aspx#securitybarriers_topic2) |
| <span data-ttu-id="316fd-362">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-362">**Steps**</span></span> | <span data-ttu-id="316fd-363">CSRF aanvallen in het webformulier op basis van toepassingen kunnen worden verholpen door ViewStateUserKey in te stellen op een willekeurige tekenreeks varieert voor elke gebruiker - gebruikers-ID of beter nog, de sessie-ID.</span><span class="sxs-lookup"><span data-stu-id="316fd-363">CSRF attacks in WebForm based applications can be mitigated by setting ViewStateUserKey to a random string that varies for each user - user ID or, better yet, session ID.</span></span> <span data-ttu-id="316fd-364">Sessie-ID is veel beter geschikt zijn voor een aantal technische en sociale oorzaken hebben, omdat een sessie-ID onvoorspelbare, is een time-out optreedt en varieert op basis van een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="316fd-364">For a number of technical and social reasons, session ID is a much better fit because a session ID is unpredictable, times out, and varies on a per-user basis.</span></span>|

### <a name="example"></a><span data-ttu-id="316fd-365">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-365">Example</span></span>
<span data-ttu-id="316fd-366">Dit is de code hoeft te hebben in alle pagina's:</span><span class="sxs-lookup"><span data-stu-id="316fd-366">Here's the code you need to have in all of your pages:</span></span>
```C#
void Page_Init (object sender, EventArgs e) {
   ViewStateUserKey = Session.SessionID;
   :
}
```

## <span data-ttu-id="316fd-367"><a id="inactivity-lifetime"></a>Sessie voor inactiviteit levensduur instellen</span><span class="sxs-lookup"><span data-stu-id="316fd-367"><a id="inactivity-lifetime"></a>Set up session for inactivity lifetime</span></span>

| <span data-ttu-id="316fd-368">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-368">Title</span></span>                   | <span data-ttu-id="316fd-369">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-369">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-370">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-370">**Component**</span></span>               | <span data-ttu-id="316fd-371">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="316fd-371">Web Application</span></span> | 
| <span data-ttu-id="316fd-372">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-372">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-373">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-373">Build</span></span> |  
| <span data-ttu-id="316fd-374">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-374">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-375">Algemene</span><span class="sxs-lookup"><span data-stu-id="316fd-375">Generic</span></span> |
| <span data-ttu-id="316fd-376">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-376">**Attributes**</span></span>              | <span data-ttu-id="316fd-377">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-377">N/A</span></span>  |
| <span data-ttu-id="316fd-378">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-378">**References**</span></span>              | <span data-ttu-id="316fd-379">[De eigenschap HttpSessionState.Timeout](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span><span class="sxs-lookup"><span data-stu-id="316fd-379">[HttpSessionState.Timeout Property](https://msdn.microsoft.com/library/system.web.sessionstate.httpsessionstate.timeout(v=vs.110).aspx)</span></span> |
| <span data-ttu-id="316fd-380">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-380">**Steps**</span></span> | <span data-ttu-id="316fd-381">Sessietime-out vertegenwoordigt de gebeurtenis die optreedt wanneer een gebruiker niet voert geen actie op een website tijdens een interval van (gedefinieerd door de webserver).</span><span class="sxs-lookup"><span data-stu-id="316fd-381">Session timeout represents the event occurring when a user does not perform any action on a web site during a interval (defined by web server).</span></span> <span data-ttu-id="316fd-382">De gebeurtenis aan serverzijde, de status van de gebruikerssessie wijzigen naar 'ongeldig' (bijvoorbeeld ' niet meer gebruikt') en dat de webserver vernietiging (verwijderen van alle gegevens die zijn opgenomen in de App).</span><span class="sxs-lookup"><span data-stu-id="316fd-382">The event, on server side, change the status of the user session to 'invalid' (for example  "not used anymore") and instruct the web server to destroy it (deleting all data contained into it).</span></span> <span data-ttu-id="316fd-383">Het volgende codevoorbeeld wordt de time-out van sessie-kenmerk ingesteld op 15 minuten in het bestand Web.config.</span><span class="sxs-lookup"><span data-stu-id="316fd-383">The following code example sets the timeout session attribute to 15 minutes in the Web.config file.</span></span>|

### <a name="example"></a><span data-ttu-id="316fd-384">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-384">Example</span></span>
<span data-ttu-id="316fd-385">'''XML-code <configuration> < system.web > <sessionState mode="InProc" cookieless="true" timeout="15" /> < /system.web ></configuration></span><span class="sxs-lookup"><span data-stu-id="316fd-385">``\`XML code <configuration> <system.web> <sessionState mode="InProc" cookieless="true" timeout="15" /> </system.web> </configuration></span></span>
```

## <a id="threat-detection"></a>Enable Threat detection on Azure SQL
```

| <span data-ttu-id="316fd-386">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-386">Title</span></span>                   | <span data-ttu-id="316fd-387">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-387">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-388">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-388">**Component**</span></span>               | <span data-ttu-id="316fd-389">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="316fd-389">Web Application</span></span> | 
| <span data-ttu-id="316fd-390">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-390">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-391">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-391">Build</span></span> |  
| <span data-ttu-id="316fd-392">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-392">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-393">Web Forms</span><span class="sxs-lookup"><span data-stu-id="316fd-393">Web Forms</span></span> |
| <span data-ttu-id="316fd-394">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-394">**Attributes**</span></span>              | <span data-ttu-id="316fd-395">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-395">N/A</span></span>  |
| <span data-ttu-id="316fd-396">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-396">**References**</span></span>              | <span data-ttu-id="316fd-397">[Element vormt voor verificatie (ASP.NET-instellingenschema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="316fd-397">[forms Element for authentication (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/1d3t3c61(v=vs.100).aspx)</span></span> |
| <span data-ttu-id="316fd-398">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-398">**Steps**</span></span> | <span data-ttu-id="316fd-399">De time-out van de cookie Formulierverificatieticket instelt op 15 minuten</span><span class="sxs-lookup"><span data-stu-id="316fd-399">Set the Forms Authentication Ticket cookie timeout to 15 minutes</span></span>|

### <a name="example"></a><span data-ttu-id="316fd-400">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-400">Example</span></span>
<span data-ttu-id="316fd-401">'''XML-code<forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span><span class="sxs-lookup"><span data-stu-id="316fd-401">``\`XML code <forms  name=".ASPXAUTH" loginUrl="login.aspx"  defaultUrl="default.aspx" protection="All" timeout="15" path="/" requireSSL="true" slidingExpiration="true"/>
</forms></span></span>
```

| Title                   | Details      |
| ----------------------- | ------------ |
| **Component**               | Web Application | 
| **SDL Phase**               | Build |  
| **Applicable Technologies** | Web Forms, MVC5 |
| **Attributes**              | EnvironmentType - OnPrem |
| **References**              | [asdeqa](https://skf.azurewebsites.net/Mitigations/Details/wefr) |
| **Steps** | When the web application is Relying Party and ADFS is the STS, the lifetime of the authentication cookies - FedAuth tokens - can be set by the following configuration in web.config:|

### Example
```XML
  <system.identityModel.services>
    <federationConfiguration>
      <!-- Set requireSsl=true; domain=application domain name used by FedAuth cookies (Ex: .gdinfra.com); -->
      <cookieHandler requireSsl="true" persistentSessionLifetime="0.0:15:0" />
      <!-- Set requireHttps=true; -->
      <wsFederation passiveRedirectEnabled="true" issuer="http://localhost:39529/" realm="https://localhost:44302/" reply="https://localhost:44302/" requireHttps="true"/>
      <!--
      Use the code below to enable encryption-decryption of claims received from ADFS. Thumbprint value varies based on the certificate being used.
      <serviceCertificate>
        <certificateReference findValue="4FBBBA33A1D11A9022A5BF3492FF83320007686A" storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" />
      </serviceCertificate>
      -->
    </federationConfiguration>
  </system.identityModel.services>
```

### <a name="example"></a><span data-ttu-id="316fd-402">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-402">Example</span></span>
<span data-ttu-id="316fd-403">De AD FS SAML uitgegeven claim ook de levensduur van token moet worden ingesteld op 15 minuten, door de volgende powershell-opdracht wordt uitgevoerd op de ADFS-server:</span><span class="sxs-lookup"><span data-stu-id="316fd-403">Also the ADFS issued SAML claim token's lifetime should be set to 15 minutes, by executing the following powershell command on the ADFS server:</span></span>
```C#
Set-ADFSRelyingPartyTrust -TargetName “<RelyingPartyWebApp>” -ClaimsProviderName @(“Active Directory”) -TokenLifetime 15 -AlwaysRequireAuthentication $true
```

## <span data-ttu-id="316fd-404"><a id="proper-app-logout"></a>Juiste afmelden van de toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="316fd-404"><a id="proper-app-logout"></a>Implement proper logout from the application</span></span>

| <span data-ttu-id="316fd-405">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-405">Title</span></span>                   | <span data-ttu-id="316fd-406">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-406">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-407">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-407">**Component**</span></span>               | <span data-ttu-id="316fd-408">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="316fd-408">Web Application</span></span> | 
| <span data-ttu-id="316fd-409">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-409">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-410">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-410">Build</span></span> |  
| <span data-ttu-id="316fd-411">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-411">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-412">Algemene</span><span class="sxs-lookup"><span data-stu-id="316fd-412">Generic</span></span> |
| <span data-ttu-id="316fd-413">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-413">**Attributes**</span></span>              | <span data-ttu-id="316fd-414">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-414">N/A</span></span>  |
| <span data-ttu-id="316fd-415">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-415">**References**</span></span>              | <span data-ttu-id="316fd-416">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-416">N/A</span></span>  |
| <span data-ttu-id="316fd-417">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-417">**Steps**</span></span> | <span data-ttu-id="316fd-418">Uitvoeren juiste afmelden van de toepassing als de gebruiker op drukt knop Afmelden.</span><span class="sxs-lookup"><span data-stu-id="316fd-418">Perform proper Sign Out from the application, when user presses log out button.</span></span> <span data-ttu-id="316fd-419">Bij het afmelden, moet toepassing vernietigen gebruikerssessie, en ook opnieuw instellen en cookie-outwaarde voor sessies, samen met opnieuw instellen en de waarde van de cookie verificatie nullifying ongeldig verklaard.</span><span class="sxs-lookup"><span data-stu-id="316fd-419">Upon logout, application should destroy user's session, and also reset and nullify session cookie value, along with resetting and nullifying authentication cookie value.</span></span> <span data-ttu-id="316fd-420">Ook wanneer meerdere sessies zijn gekoppeld aan een enkele gebruikers-id, moeten ze worden gezamenlijk afgesloten aan de serverzijde op time-out of meld u af.</span><span class="sxs-lookup"><span data-stu-id="316fd-420">Also, when multiple sessions are tied to a single user identity, they must be collectively terminated on the server side at timeout or logout.</span></span> <span data-ttu-id="316fd-421">Ten slotte zorgen ervoor dat afmelding functionaliteit beschikbaar op elke pagina.</span><span class="sxs-lookup"><span data-stu-id="316fd-421">Lastly, ensure that Logout functionality is available on every page.</span></span> |

## <span data-ttu-id="316fd-422"><a id="csrf-api"></a>Beperken dat Cross-Site aanvragen kunnen worden vervalst (CSRF) aanvallen op ASP.NET Web-API 's</span><span class="sxs-lookup"><span data-stu-id="316fd-422"><a id="csrf-api"></a>Mitigate against Cross-Site Request Forgery (CSRF) attacks on ASP.NET Web APIs</span></span>

| <span data-ttu-id="316fd-423">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-423">Title</span></span>                   | <span data-ttu-id="316fd-424">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-424">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-425">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-425">**Component**</span></span>               | <span data-ttu-id="316fd-426">Web-API</span><span class="sxs-lookup"><span data-stu-id="316fd-426">Web API</span></span> | 
| <span data-ttu-id="316fd-427">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-427">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-428">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-428">Build</span></span> |  
| <span data-ttu-id="316fd-429">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-429">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-430">Algemene</span><span class="sxs-lookup"><span data-stu-id="316fd-430">Generic</span></span> |
| <span data-ttu-id="316fd-431">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-431">**Attributes**</span></span>              | <span data-ttu-id="316fd-432">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-432">N/A</span></span>  |
| <span data-ttu-id="316fd-433">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-433">**References**</span></span>              | <span data-ttu-id="316fd-434">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-434">N/A</span></span>  |
| <span data-ttu-id="316fd-435">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-435">**Steps**</span></span> | <span data-ttu-id="316fd-436">Aanvraagvervalsing op meerdere sites (CSRF of XSRF) is een type van een aanval waarbij een aanvaller acties in de beveiligingscontext van de vastgestelde sessie een andere gebruiker op een website kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="316fd-436">Cross-site request forgery (CSRF or XSRF) is a type of attack in which an attacker can carry out actions in the security context of a different user's established session on a web site.</span></span> <span data-ttu-id="316fd-437">Het doel is om te wijzigen of verwijderen van inhoud, als voor de betreffende website uitsluitend sessiecookies ontvangen request verifiëren.</span><span class="sxs-lookup"><span data-stu-id="316fd-437">The goal is to modify or delete content, if the targeted web site relies exclusively on session cookies to authenticate received request.</span></span> <span data-ttu-id="316fd-438">Een aanvaller kan deze kwetsbaarheid misbruiken met het ophalen van de browser een URL met een opdracht laden van een kwetsbaar site waarop de gebruiker is aangemeld in een andere gebruiker.</span><span class="sxs-lookup"><span data-stu-id="316fd-438">An attacker could exploit this vulnerability by getting a different user's browser to load a URL with a command from a vulnerable site on which the user is already logged in.</span></span> <span data-ttu-id="316fd-439">Er zijn veel manieren voor aanvallers om u te doen, zoals door die als host fungeert voor een andere website die wordt een resource van de server kwetsbaar wordt geladen, of voor het verkrijgen van de gebruiker op een koppeling te klikken.</span><span class="sxs-lookup"><span data-stu-id="316fd-439">There are many ways for an attacker to do that, such as by hosting a different web site that loads a resource from the vulnerable server, or getting the user to click a link.</span></span> <span data-ttu-id="316fd-440">De aanval kan worden voorkomen als de server een extra token naar de client verzendt vereist dat de client die token opnemen in alle toekomstige aanvragen en verifieert dat alle toekomstige aanvragen een token dat betrekking op de huidige sessie bevatten, heeft zoals met behulp van de ASP.NET AntiForgeryToken of ViewState.</span><span class="sxs-lookup"><span data-stu-id="316fd-440">The attack can be prevented if the server sends an additional token to the client, requires the client to include that token in all future requests, and verifies that all future requests include a token that pertains to the current session, such as by using the ASP.NET AntiForgeryToken or ViewState.</span></span> |

| <span data-ttu-id="316fd-441">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-441">Title</span></span>                   | <span data-ttu-id="316fd-442">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-442">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-443">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-443">**Component**</span></span>               | <span data-ttu-id="316fd-444">Web-API</span><span class="sxs-lookup"><span data-stu-id="316fd-444">Web API</span></span> | 
| <span data-ttu-id="316fd-445">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-445">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-446">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-446">Build</span></span> |  
| <span data-ttu-id="316fd-447">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-447">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-448">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="316fd-448">MVC5, MVC6</span></span> |
| <span data-ttu-id="316fd-449">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-449">**Attributes**</span></span>              | <span data-ttu-id="316fd-450">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="316fd-450">N/A</span></span>  |
| <span data-ttu-id="316fd-451">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-451">**References**</span></span>              | [<span data-ttu-id="316fd-452">Het voorkomen van Aanvraagvervalsing op meerdere sites (CSRF) aanvallen in ASP.NET Web-API</span><span class="sxs-lookup"><span data-stu-id="316fd-452">Preventing Cross-Site Request Forgery (CSRF) Attacks in ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks) |
| <span data-ttu-id="316fd-453">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-453">**Steps**</span></span> | <span data-ttu-id="316fd-454">Anti-CSRF en AJAX: het token van het formulier een probleem voor AJAX-aanvragen kan worden, omdat een AJAX-aanvraag JSON-gegevens, geen HTML-formuliergegevens kan verzenden.</span><span class="sxs-lookup"><span data-stu-id="316fd-454">Anti-CSRF and AJAX: The form token can be a problem for AJAX requests, because an AJAX request might send JSON data, not HTML form data.</span></span> <span data-ttu-id="316fd-455">Eén oplossing is voor het verzenden van de tokens in een aangepaste HTTP-header.</span><span class="sxs-lookup"><span data-stu-id="316fd-455">One solution is to send the tokens in a custom HTTP header.</span></span> <span data-ttu-id="316fd-456">De volgende code Razor syntaxis wordt gebruikt voor het genereren van de tokens en vervolgens de tokens toegevoegd aan een AJAX-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="316fd-456">The following code uses Razor syntax to generate the tokens, and then adds the tokens to an AJAX request.</span></span> |

### <a name="example"></a><span data-ttu-id="316fd-457">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-457">Example</span></span>
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

### <a name="example"></a><span data-ttu-id="316fd-458">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-458">Example</span></span>
<span data-ttu-id="316fd-459">Wanneer u de aanvraag verwerkt, moet u de tokens extraheren uit de aanvraagheader.</span><span class="sxs-lookup"><span data-stu-id="316fd-459">When you process the request, extract the tokens from the request header.</span></span> <span data-ttu-id="316fd-460">Vervolgens roept de methode AntiForgery.Validate voor het valideren van de tokens.</span><span class="sxs-lookup"><span data-stu-id="316fd-460">Then call the AntiForgery.Validate method to validate the tokens.</span></span> <span data-ttu-id="316fd-461">De methode Validate genereert een uitzondering als de tokens niet geldig zijn.</span><span class="sxs-lookup"><span data-stu-id="316fd-461">The Validate method throws an exception if the tokens are not valid.</span></span>
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

### <a name="example"></a><span data-ttu-id="316fd-462">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-462">Example</span></span>
<span data-ttu-id="316fd-463">Anti-CSRF en formulieren ASP.NET MVC - gebruikmaken van de Help-methode AntiForgeryToken op weergaven; bijvoorbeeld, een Html.AntiForgeryToken() in het formulier plaatsen</span><span class="sxs-lookup"><span data-stu-id="316fd-463">Anti-CSRF and ASP.NET MVC forms - Use the AntiForgeryToken helper method on Views; put an Html.AntiForgeryToken() into the form, for example,</span></span>
```C#
@using (Html.BeginForm("UserProfile", "SubmitUpdate")) { 
    @Html.ValidationSummary(true) 
    @Html.AntiForgeryToken()
    <fieldset> 
}
```

### <a name="example"></a><span data-ttu-id="316fd-464">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-464">Example</span></span>
<span data-ttu-id="316fd-465">Het bovenstaande voorbeeld wordt ongeveer de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="316fd-465">The example above will output something like the following:</span></span>
```C#
<form action="/UserProfile/SubmitUpdate" method="post">
    <input name="__RequestVerificationToken" type="hidden" value="saTFWpkKN0BYazFtN6c4YbZAmsEwG0srqlUqqloi/fVgeV2ciIFVmelvzwRZpArs" />
    <!-- rest of form goes here -->
</form>
```

### <a name="example"></a><span data-ttu-id="316fd-466">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-466">Example</span></span>
<span data-ttu-id="316fd-467">Op hetzelfde moment biedt Html.AntiForgeryToken() de bezoeker een cookie met de naam __RequestVerificationToken met dezelfde waarde als de willekeurige verborgen waarde hierboven weergegeven.</span><span class="sxs-lookup"><span data-stu-id="316fd-467">At the same time, Html.AntiForgeryToken() gives the visitor a cookie called __RequestVerificationToken, with the same value as the random hidden value shown above.</span></span> <span data-ttu-id="316fd-468">Vervolgens voegt u het filter [ValidateAntiForgeryToken] aan doelmethode actie voor het valideren van een binnenkomende Formulierbericht.</span><span class="sxs-lookup"><span data-stu-id="316fd-468">Next, to validate an incoming form post, add the [ValidateAntiForgeryToken] filter to the target action method.</span></span> <span data-ttu-id="316fd-469">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="316fd-469">For example:</span></span>
```
[ValidateAntiForgeryToken]
public ViewResult SubmitUpdate()
{
// ... etc.
}
```
<span data-ttu-id="316fd-470">Autorisatiefilter die of controleert:</span><span class="sxs-lookup"><span data-stu-id="316fd-470">Authorization filter that checks that:</span></span>
* <span data-ttu-id="316fd-471">De binnenkomende aanvraag heeft een cookie met de naam __RequestVerificationToken</span><span class="sxs-lookup"><span data-stu-id="316fd-471">The incoming request has a cookie called __RequestVerificationToken</span></span>
* <span data-ttu-id="316fd-472">De binnenkomende aanvraag heeft een `Request.Form` vermelding __RequestVerificationToken aangeroepen</span><span class="sxs-lookup"><span data-stu-id="316fd-472">The incoming request has a `Request.Form` entry called __RequestVerificationToken</span></span>
* <span data-ttu-id="316fd-473">Deze cookie en `Request.Form` waarden overeenkomen, ervan uitgaande dat alle goed is, de aanvraag wordt verwerkt via die normaal werken.</span><span class="sxs-lookup"><span data-stu-id="316fd-473">These cookie and `Request.Form` values match Assuming all is well, the request goes through as normal.</span></span> <span data-ttu-id="316fd-474">Maar als dit niet het geval is, klikt u vervolgens een Autorisatiefout met het bericht 'een vereiste anti-vervalsingstoken is niet opgegeven of is ongeldig'.</span><span class="sxs-lookup"><span data-stu-id="316fd-474">But if not, then an authorization failure with message “A required anti-forgery token was not supplied or was invalid”.</span></span>

| <span data-ttu-id="316fd-475">Titel</span><span class="sxs-lookup"><span data-stu-id="316fd-475">Title</span></span>                   | <span data-ttu-id="316fd-476">Details</span><span class="sxs-lookup"><span data-stu-id="316fd-476">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="316fd-477">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="316fd-477">**Component**</span></span>               | <span data-ttu-id="316fd-478">Web-API</span><span class="sxs-lookup"><span data-stu-id="316fd-478">Web API</span></span> | 
| <span data-ttu-id="316fd-479">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="316fd-479">**SDL Phase**</span></span>               | <span data-ttu-id="316fd-480">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="316fd-480">Build</span></span> |  
| <span data-ttu-id="316fd-481">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="316fd-481">**Applicable Technologies**</span></span> | <span data-ttu-id="316fd-482">MVC5, MVC6</span><span class="sxs-lookup"><span data-stu-id="316fd-482">MVC5, MVC6</span></span> |
| <span data-ttu-id="316fd-483">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="316fd-483">**Attributes**</span></span>              | <span data-ttu-id="316fd-484">ID-Provider - ADFS, identiteitsprovider - Azure AD</span><span class="sxs-lookup"><span data-stu-id="316fd-484">Identity Provider - ADFS, Identity Provider - Azure AD</span></span> |
| <span data-ttu-id="316fd-485">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="316fd-485">**References**</span></span>              | [<span data-ttu-id="316fd-486">Een Web-API met afzonderlijke Accounts en lokale aanmelding in ASP.NET Web-API 2.2 beveiligen</span><span class="sxs-lookup"><span data-stu-id="316fd-486">Secure a Web API with Individual Accounts and Local Login in ASP.NET Web API 2.2</span></span>](http://www.asp.net/web-api/overview/security/individual-accounts-in-web-api) |
| <span data-ttu-id="316fd-487">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="316fd-487">**Steps**</span></span> | <span data-ttu-id="316fd-488">Als de Web-API is beveiligd met OAuth 2.0, vervolgens een bearer-token in autorisatie-header voor aanvraag verwacht en verleent toegang tot de aanvraag alleen als het token geldig is.</span><span class="sxs-lookup"><span data-stu-id="316fd-488">If the Web API is secured using OAuth 2.0, then it expects a bearer token in Authorization request header and grants access to the request only if the token is valid.</span></span> <span data-ttu-id="316fd-489">In tegenstelling tot op basis van Cookieverificatie koppel browsers geen bearer-tokens op aanvragen.</span><span class="sxs-lookup"><span data-stu-id="316fd-489">Unlike cookie based authentication, browsers do not attach the bearer tokens to requests.</span></span> <span data-ttu-id="316fd-490">De aanvragende client moet expliciet de bearer-token in de aanvraagheader te koppelen.</span><span class="sxs-lookup"><span data-stu-id="316fd-490">The requesting client needs to explicitly attach the bearer token in the request header.</span></span> <span data-ttu-id="316fd-491">Daarom voor ASP.NET Web API's beveiligd met OAuth 2.0-bearer-tokens worden beschouwd als bij de bescherming tegen aanvallen CSRF.</span><span class="sxs-lookup"><span data-stu-id="316fd-491">Therefore, for ASP.NET Web APIs protected using OAuth 2.0, bearer tokens are considered as a defense against CSRF attacks.</span></span> <span data-ttu-id="316fd-492">Houd er rekening mee dat als het MVC-gedeelte van de toepassing gebruikmaakt van formulierverificatie (dat wil zeggen, maakt gebruik van cookies), ter voorkoming tokens moeten worden gebruikt door de MVC-web-app.</span><span class="sxs-lookup"><span data-stu-id="316fd-492">Please note that if the MVC portion of the application uses forms authentication (i.e., uses cookies), anti-forgery tokens have to be used by the MVC web app.</span></span> |

### <a name="example"></a><span data-ttu-id="316fd-493">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="316fd-493">Example</span></span>
<span data-ttu-id="316fd-494">De Web-API heeft om te worden gesteld te vertrouwen alleen op bearer-tokens en niet voor cookies.</span><span class="sxs-lookup"><span data-stu-id="316fd-494">The Web API has to be informed to rely ONLY on bearer tokens and not on cookies.</span></span> <span data-ttu-id="316fd-495">Het kan worden gedaan door de volgende configuratie in `WebApiConfig.Register` methode: '''C-Sharp code config. SuppressDefaultHostAuthentication(); configuratie. Filters.Add (nieuwe HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span><span class="sxs-lookup"><span data-stu-id="316fd-495">It can be done by the following configuration in `WebApiConfig.Register` method: ``\`C-Sharp code config.SuppressDefaultHostAuthentication(); config.Filters.Add(new HostAuthenticationFilter(OAuthDefaults.AuthenticationType));</span></span>
```
The SuppressDefaultHostAuthentication method tells Web API to ignore any authentication that happens before the request reaches the Web API pipeline, either by IIS or by OWIN middleware. That way, we can restrict Web API to authenticate only using bearer tokens.
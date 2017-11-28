---
title: aaaClient en server SDK-versies in Mobile Apps- en Mobile Services | Microsoft Docs
description: Lijst met client-SDK's en compatibiliteit met versies van de server-SDK voor Mobile Services en Azure Mobile Apps
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="9eda1-103">Client- en versiebeheer in Mobile Apps- en Mobile Services</span><span class="sxs-lookup"><span data-stu-id="9eda1-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="9eda1-104">Hallo meest recente versie van Azure Mobile Services is Hallo **Mobile Apps** functie van Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="9eda1-104">hello latest version of Azure Mobile Services is hello **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="9eda1-105">Hallo mobiele Apps-client en server SDK's oorspronkelijk zijn gebaseerd op die in Mobile Services, maar ze zijn *niet* compatibel met elkaar.</span><span class="sxs-lookup"><span data-stu-id="9eda1-105">hello Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="9eda1-106">Dat wil zeggen, moet u een *Mobile Apps* SDK voor clients met een *Mobile Apps* server SDK en op dezelfde manier voor *Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="9eda1-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="9eda1-107">Dit contract wordt afgedwongen via een speciale headerwaarde die wordt gebruikt door Hallo-client en server SDK's, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="9eda1-107">This contract is enforced through a special header value used by hello client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="9eda1-108">Opmerking: als dit document tooa verwijst *Mobile Services* backend, hoeft deze niet per se toobe gehost in Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="9eda1-108">Note: whenever this document refers tooa *Mobile Services* backend, it does not necessarily need toobe hosted on Mobile Services.</span></span> <span data-ttu-id="9eda1-109">Het is nu mogelijk toomigrate een mobiele service toorun op App Service zonder codewijzigingen, maar zou Hallo-service nog steeds gebruikmaken van *Mobile Services* SDK-versies.</span><span class="sxs-lookup"><span data-stu-id="9eda1-109">It is now possible toomigrate a mobile service toorun on App Service without any code changes, but hello service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="9eda1-110">informatie over toolearn migreren tooApp Service zonder code wijzigen, Zie Hallo artikel [migreren van een tooAzure Mobile Service-App Service].</span><span class="sxs-lookup"><span data-stu-id="9eda1-110">toolearn more about migrating tooApp Service without any code changes, see hello article [Migrate a Mobile Service tooAzure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="9eda1-111">Header-specificatie</span><span class="sxs-lookup"><span data-stu-id="9eda1-111">Header specification</span></span>
<span data-ttu-id="9eda1-112">Hallo sleutel `ZUMO-API-VERSION` in Hallo HTTP-koptekst of queryreeks Hallo mag worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9eda1-112">hello key `ZUMO-API-VERSION` may be specified in either hello HTTP header or hello query string.</span></span> <span data-ttu-id="9eda1-113">Hallo-waarde is een versietekenreeks in formulier Hallo **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="9eda1-113">hello value is a version string in hello form **x.y.z**.</span></span>

<span data-ttu-id="9eda1-114">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9eda1-114">For example:</span></span>

<span data-ttu-id="9eda1-115">Https://service.azurewebsites.net/tables/TodoItem ophalen</span><span class="sxs-lookup"><span data-stu-id="9eda1-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="9eda1-116">HEADERS: ZUMO-API-VERSIE: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="9eda1-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="9eda1-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="9eda1-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="9eda1-118">Buiten-versiecontrole uitschakelen</span><span class="sxs-lookup"><span data-stu-id="9eda1-118">Opting out of version checking</span></span>
<span data-ttu-id="9eda1-119">U kunt ervoor kiezen niet versie controleren door een waarde van **true** voor app-instelling Hallo **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="9eda1-119">You can opt out of version checking by setting a value of **true** for hello app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="9eda1-120">Geef dit in uw web.config of in Hallo sectie Toepassingsinstellingen hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="9eda1-120">Specify this either in your web.config or in hello Application Settings section of hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="9eda1-121">Er zijn een aantal gedragswijzigingen tussen Mobile Services en mobiele Apps, met name in Hallo gebieden van het offline synchroniseren, verificatie en pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="9eda1-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in hello areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="9eda1-122">U moet alleen versiecontrole na volledige testen tooensure dat deze wijzigingen het van uw app-functionaliteit niet breken afmelden.</span><span class="sxs-lookup"><span data-stu-id="9eda1-122">You should only opt out of version checking after complete testing tooensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="9eda1-123">Samenvatting van compatibiliteit voor alle versies</span><span class="sxs-lookup"><span data-stu-id="9eda1-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="9eda1-124">Hallo diagram hieronder toont Hallo compatibiliteit tussen alle typen van client en server.</span><span class="sxs-lookup"><span data-stu-id="9eda1-124">hello chart below shows hello compatibility between all client and server types.</span></span> <span data-ttu-id="9eda1-125">Een back-end is geclassificeerd als beide Mobile **Services** of Mobile **Apps** op basis van Hallo server SDK die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9eda1-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on hello server SDK that it uses.</span></span>

|  | <span data-ttu-id="9eda1-126">**Mobile Services** Node.js- of .NET</span><span class="sxs-lookup"><span data-stu-id="9eda1-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="9eda1-127">**Mobiele Apps** Node.js- of .NET</span><span class="sxs-lookup"><span data-stu-id="9eda1-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9eda1-128">[Mobile Services-clients]</span><span class="sxs-lookup"><span data-stu-id="9eda1-128">[Mobile Services clients]</span></span> |<span data-ttu-id="9eda1-129">OK</span><span class="sxs-lookup"><span data-stu-id="9eda1-129">Ok</span></span> |<span data-ttu-id="9eda1-130">Fout\*</span><span class="sxs-lookup"><span data-stu-id="9eda1-130">Error\*</span></span> |
| <span data-ttu-id="9eda1-131">[Clients voor mobiele Apps]</span><span class="sxs-lookup"><span data-stu-id="9eda1-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="9eda1-132">Fout\*</span><span class="sxs-lookup"><span data-stu-id="9eda1-132">Error\*</span></span> |<span data-ttu-id="9eda1-133">OK</span><span class="sxs-lookup"><span data-stu-id="9eda1-133">Ok</span></span> |

<span data-ttu-id="9eda1-134">\*Dit kan worden beheerd door te geven **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="9eda1-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="9eda1-135"><a name="1.0.0"></a>Mobile Services-client en server</span><span class="sxs-lookup"><span data-stu-id="9eda1-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="9eda1-136">Hallo client-SDK's in onderstaande tabel voor Hallo compatibel zijn met **Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="9eda1-136">hello client SDKs in hello table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="9eda1-137">Opmerking: Hallo Mobile Services-client-SDK's *niet* een headerwaarde verzenden voor `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="9eda1-137">Note: hello Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="9eda1-138">Als het Hallo-service ontvangt deze kop- of queryreekswaarde, een fout geretourneerd, tenzij u expliciet uit zoals hierboven beschreven hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="9eda1-138">If hello service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="9eda1-139"><a name="MobileServicesClients"></a>Mobiele *Services* client-SDK's</span><span class="sxs-lookup"><span data-stu-id="9eda1-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="9eda1-140">Clientplatform</span><span class="sxs-lookup"><span data-stu-id="9eda1-140">Client platform</span></span> | <span data-ttu-id="9eda1-141">Versie</span><span class="sxs-lookup"><span data-stu-id="9eda1-141">Version</span></span> | <span data-ttu-id="9eda1-142">De versieheaderwaarde</span><span class="sxs-lookup"><span data-stu-id="9eda1-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9eda1-143">Beheerde client (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="9eda1-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="9eda1-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="9eda1-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="9eda1-145">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="9eda1-145">n/a</span></span> |
| <span data-ttu-id="9eda1-146">iOS</span><span class="sxs-lookup"><span data-stu-id="9eda1-146">iOS</span></span> |[<span data-ttu-id="9eda1-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="9eda1-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="9eda1-148">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="9eda1-148">n/a</span></span> |
| <span data-ttu-id="9eda1-149">Android</span><span class="sxs-lookup"><span data-stu-id="9eda1-149">Android</span></span> |[<span data-ttu-id="9eda1-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="9eda1-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="9eda1-151">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="9eda1-151">n/a</span></span> |
| <span data-ttu-id="9eda1-152">HTML</span><span class="sxs-lookup"><span data-stu-id="9eda1-152">HTML</span></span> |[<span data-ttu-id="9eda1-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="9eda1-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="9eda1-154">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="9eda1-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="9eda1-155">Mobiele *Services* server SDK's</span><span class="sxs-lookup"><span data-stu-id="9eda1-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="9eda1-156">Server-platform</span><span class="sxs-lookup"><span data-stu-id="9eda1-156">Server platform</span></span> | <span data-ttu-id="9eda1-157">Versie</span><span class="sxs-lookup"><span data-stu-id="9eda1-157">Version</span></span> | <span data-ttu-id="9eda1-158">Geaccepteerde versie-header</span><span class="sxs-lookup"><span data-stu-id="9eda1-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9eda1-159">.NET</span><span class="sxs-lookup"><span data-stu-id="9eda1-159">.NET</span></span> |[<span data-ttu-id="9eda1-160">WindowsAzure.MobileServices.Backend.* versie 1.0.x</span><span class="sxs-lookup"><span data-stu-id="9eda1-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="9eda1-161">** Geen versiekop **</span><span class="sxs-lookup"><span data-stu-id="9eda1-161">**No version header **</span></span> |
| <span data-ttu-id="9eda1-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="9eda1-162">Node.js</span></span> |<span data-ttu-id="9eda1-163">(binnenkort)</span><span class="sxs-lookup"><span data-stu-id="9eda1-163">(coming soon)</span></span> |<span data-ttu-id="9eda1-164">**Er is geen versie-header**</span><span class="sxs-lookup"><span data-stu-id="9eda1-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="9eda1-165">Gedrag van de back-ends voor Mobile Services</span><span class="sxs-lookup"><span data-stu-id="9eda1-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="9eda1-166">ZUMO-API-VERSIE</span><span class="sxs-lookup"><span data-stu-id="9eda1-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="9eda1-167">Waarde van MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="9eda1-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="9eda1-168">Antwoord</span><span class="sxs-lookup"><span data-stu-id="9eda1-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9eda1-169">Niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="9eda1-169">Not specified</span></span> |<span data-ttu-id="9eda1-170">Alle</span><span class="sxs-lookup"><span data-stu-id="9eda1-170">Any</span></span> |<span data-ttu-id="9eda1-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="9eda1-171">200 - OK</span></span> |
| <span data-ttu-id="9eda1-172">Een willekeurige waarde</span><span class="sxs-lookup"><span data-stu-id="9eda1-172">Any value</span></span> |<span data-ttu-id="9eda1-173">True</span><span class="sxs-lookup"><span data-stu-id="9eda1-173">True</span></span> |<span data-ttu-id="9eda1-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="9eda1-174">200 - OK</span></span> |
| <span data-ttu-id="9eda1-175">Een willekeurige waarde</span><span class="sxs-lookup"><span data-stu-id="9eda1-175">Any value</span></span> |<span data-ttu-id="9eda1-176">ONWAAR/niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="9eda1-176">False/Not Specified</span></span> |<span data-ttu-id="9eda1-177">400 - onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="9eda1-177">400 - Bad Request</span></span> |

## <span data-ttu-id="9eda1-178"><a name="2.0.0"></a>Azure Mobile Apps-client en server</span><span class="sxs-lookup"><span data-stu-id="9eda1-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="9eda1-179"><a name="MobileAppsClients"></a>Mobiele *Apps* client-SDK's</span><span class="sxs-lookup"><span data-stu-id="9eda1-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="9eda1-180">Beginnen met de volgende versies van Hallo client SDK Hallo versiecontrole is geïntroduceerd voor **Azure Mobile Apps**:</span><span class="sxs-lookup"><span data-stu-id="9eda1-180">Version checking was introduced starting with hello following versions of hello client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="9eda1-181">Clientplatform</span><span class="sxs-lookup"><span data-stu-id="9eda1-181">Client platform</span></span> | <span data-ttu-id="9eda1-182">Versie</span><span class="sxs-lookup"><span data-stu-id="9eda1-182">Version</span></span> | <span data-ttu-id="9eda1-183">De versieheaderwaarde</span><span class="sxs-lookup"><span data-stu-id="9eda1-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9eda1-184">Beheerde client (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="9eda1-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="9eda1-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9eda1-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="9eda1-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9eda1-186">2.0.0</span></span> |
| <span data-ttu-id="9eda1-187">iOS</span><span class="sxs-lookup"><span data-stu-id="9eda1-187">iOS</span></span> |[<span data-ttu-id="9eda1-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="9eda1-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="9eda1-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9eda1-189">2.0.0</span></span> |
| <span data-ttu-id="9eda1-190">Android</span><span class="sxs-lookup"><span data-stu-id="9eda1-190">Android</span></span> |[<span data-ttu-id="9eda1-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="9eda1-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="9eda1-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="9eda1-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="9eda1-193">Mobiele *Apps* server SDK's</span><span class="sxs-lookup"><span data-stu-id="9eda1-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="9eda1-194">Versiecontrole is opgenomen in de volgende server SDK-versies:</span><span class="sxs-lookup"><span data-stu-id="9eda1-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="9eda1-195">Server-platform</span><span class="sxs-lookup"><span data-stu-id="9eda1-195">Server platform</span></span> | <span data-ttu-id="9eda1-196">SDK</span><span class="sxs-lookup"><span data-stu-id="9eda1-196">SDK</span></span> | <span data-ttu-id="9eda1-197">Geaccepteerde versie-header</span><span class="sxs-lookup"><span data-stu-id="9eda1-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9eda1-198">.NET</span><span class="sxs-lookup"><span data-stu-id="9eda1-198">.NET</span></span> |[<span data-ttu-id="9eda1-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="9eda1-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="9eda1-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9eda1-200">2.0.0</span></span> |
| <span data-ttu-id="9eda1-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="9eda1-201">Node.js</span></span> |[<span data-ttu-id="9eda1-202">Azure mobile apps)</span><span class="sxs-lookup"><span data-stu-id="9eda1-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="9eda1-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="9eda1-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="9eda1-204">Gedrag van de back-ends voor mobiele Apps</span><span class="sxs-lookup"><span data-stu-id="9eda1-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="9eda1-205">ZUMO-API-VERSIE</span><span class="sxs-lookup"><span data-stu-id="9eda1-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="9eda1-206">Waarde van MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="9eda1-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="9eda1-207">Antwoord</span><span class="sxs-lookup"><span data-stu-id="9eda1-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9eda1-208">x.y.z of Null zijn</span><span class="sxs-lookup"><span data-stu-id="9eda1-208">x.y.z or Null</span></span> |<span data-ttu-id="9eda1-209">True</span><span class="sxs-lookup"><span data-stu-id="9eda1-209">True</span></span> |<span data-ttu-id="9eda1-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="9eda1-210">200 - OK</span></span> |
| <span data-ttu-id="9eda1-211">Null</span><span class="sxs-lookup"><span data-stu-id="9eda1-211">Null</span></span> |<span data-ttu-id="9eda1-212">ONWAAR/niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="9eda1-212">False/Not Specified</span></span> |<span data-ttu-id="9eda1-213">400 - onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="9eda1-213">400 - Bad Request</span></span> |
| <span data-ttu-id="9eda1-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="9eda1-214">1.x.y</span></span> |<span data-ttu-id="9eda1-215">ONWAAR/niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="9eda1-215">False/Not Specified</span></span> |<span data-ttu-id="9eda1-216">400 - onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="9eda1-216">400 - Bad Request</span></span> |
| <span data-ttu-id="9eda1-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="9eda1-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="9eda1-218">ONWAAR/niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="9eda1-218">False/Not Specified</span></span> |<span data-ttu-id="9eda1-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="9eda1-219">200 - OK</span></span> |
| <span data-ttu-id="9eda1-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="9eda1-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="9eda1-221">ONWAAR/niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="9eda1-221">False/Not Specified</span></span> |<span data-ttu-id="9eda1-222">400 - onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="9eda1-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9eda1-223">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9eda1-223">Next Steps</span></span>
* <span data-ttu-id="9eda1-224">[migreren van een tooAzure Mobile Service-App Service]</span><span class="sxs-lookup"><span data-stu-id="9eda1-224">[Migrate a Mobile Service tooAzure App Service]</span></span>

[Mobile Services-clients]: #MobileServicesClients
[Clients voor mobiele Apps]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[migreren van een tooAzure Mobile Service-App Service]: app-service-mobile-migrating-from-mobile-services.md

---
title: Client en server SDK-versies in Mobile Apps- en Mobile Services | Microsoft Docs
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
ms.openlocfilehash: f79e819b1547f81498ea213858faf3c75e374782
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a><span data-ttu-id="6dc04-103">Client- en versiebeheer in Mobile Apps- en Mobile Services</span><span class="sxs-lookup"><span data-stu-id="6dc04-103">Client and server versioning in Mobile Apps and Mobile Services</span></span>
<span data-ttu-id="6dc04-104">De meest recente versie van Azure Mobile Services is de **Mobile Apps** functie van Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="6dc04-104">The latest version of Azure Mobile Services is the **Mobile Apps** feature of Azure App Service.</span></span>

<span data-ttu-id="6dc04-105">De Mobile Apps-client en server SDK's oorspronkelijk zijn gebaseerd op die in Mobile Services, maar ze zijn *niet* compatibel met elkaar.</span><span class="sxs-lookup"><span data-stu-id="6dc04-105">The Mobile Apps client and server SDKs are originally based on those in Mobile Services, but they are *not* compatible with each other.</span></span>
<span data-ttu-id="6dc04-106">Dat wil zeggen, moet u een *Mobile Apps* SDK voor clients met een *Mobile Apps* server SDK en op dezelfde manier voor *Mobile Services*.</span><span class="sxs-lookup"><span data-stu-id="6dc04-106">That is, you must use a *Mobile Apps* client SDK with a *Mobile Apps* server SDK and similarly for *Mobile Services*.</span></span> <span data-ttu-id="6dc04-107">Dit contract wordt afgedwongen via een speciale headerwaarde die wordt gebruikt door de client en server SDK's, `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="6dc04-107">This contract is enforced through a special header value used by the client and server SDKs, `ZUMO-API-VERSION`.</span></span>

<span data-ttu-id="6dc04-108">Opmerking: als dit document verwijst naar een *Mobile Services* back-end van het niet per se hoeft te worden gehost in Mobile Services.</span><span class="sxs-lookup"><span data-stu-id="6dc04-108">Note: whenever this document refers to a *Mobile Services* backend, it does not necessarily need to be hosted on Mobile Services.</span></span> <span data-ttu-id="6dc04-109">Het is nu mogelijk om te migreren van een mobiele service worden uitgevoerd op App Service zonder codewijzigingen, maar de service nog steeds gebruikt *Mobile Services* SDK-versies.</span><span class="sxs-lookup"><span data-stu-id="6dc04-109">It is now possible to migrate a mobile service to run on App Service without any code changes, but the service would still be using *Mobile Services*  SDK versions.</span></span>

<span data-ttu-id="6dc04-110">Zie het artikel voor meer informatie over het migreren naar App Service zonder codewijzigingen [een mobiele Service migreren naar Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="6dc04-110">To learn more about migrating to App Service without any code changes, see the article [Migrate a Mobile Service to Azure App Service].</span></span>

## <a name="header-specification"></a><span data-ttu-id="6dc04-111">Header-specificatie</span><span class="sxs-lookup"><span data-stu-id="6dc04-111">Header specification</span></span>
<span data-ttu-id="6dc04-112">De sleutel `ZUMO-API-VERSION` mag worden opgegeven in de HTTP-header of de query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="6dc04-112">The key `ZUMO-API-VERSION` may be specified in either the HTTP header or the query string.</span></span> <span data-ttu-id="6dc04-113">De waarde is een versietekenreeks in het formulier **x.y.z**.</span><span class="sxs-lookup"><span data-stu-id="6dc04-113">The value is a version string in the form **x.y.z**.</span></span>

<span data-ttu-id="6dc04-114">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6dc04-114">For example:</span></span>

<span data-ttu-id="6dc04-115">Https://service.azurewebsites.net/tables/TodoItem ophalen</span><span class="sxs-lookup"><span data-stu-id="6dc04-115">GET https://service.azurewebsites.net/tables/TodoItem</span></span>

<span data-ttu-id="6dc04-116">HEADERS: ZUMO-API-VERSIE: 2.0.0</span><span class="sxs-lookup"><span data-stu-id="6dc04-116">HEADERS: ZUMO-API-VERSION: 2.0.0</span></span>

<span data-ttu-id="6dc04-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span><span class="sxs-lookup"><span data-stu-id="6dc04-117">POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0</span></span>

## <a name="opting-out-of-version-checking"></a><span data-ttu-id="6dc04-118">Buiten-versiecontrole uitschakelen</span><span class="sxs-lookup"><span data-stu-id="6dc04-118">Opting out of version checking</span></span>
<span data-ttu-id="6dc04-119">U kunt ervoor kiezen niet versie controleren door een waarde van **true** voor de app-instelling **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="6dc04-119">You can opt out of version checking by setting a value of **true** for the app setting **MS_SkipVersionCheck**.</span></span> <span data-ttu-id="6dc04-120">Geef dit in uw web.config of in de sectie Toepassingsinstellingen van de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6dc04-120">Specify this either in your web.config or in the Application Settings section of the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6dc04-121">Er zijn een aantal gedragswijzigingen tussen Mobile Services en mobiele Apps, met name op het gebied van het offline synchroniseren, verificatie en pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="6dc04-121">There are a number of behavior changes between Mobile Services and Mobile Apps, particularly in the areas of offline sync, authentication, and push notifications.</span></span> <span data-ttu-id="6dc04-122">U moet alleen versiecontrole na testen voltooien om ervoor te zorgen dat deze wijzigingen het van uw app-functionaliteit niet breken afmelden.</span><span class="sxs-lookup"><span data-stu-id="6dc04-122">You should only opt out of version checking after complete testing to ensure that these behavioral changes do not break your app's functionality.</span></span>
>
>

## <a name="summary-of-compatibility-for-all-versions"></a><span data-ttu-id="6dc04-123">Samenvatting van compatibiliteit voor alle versies</span><span class="sxs-lookup"><span data-stu-id="6dc04-123">Summary of compatibility for all versions</span></span>
<span data-ttu-id="6dc04-124">Het onderstaande diagram ziet u de compatibiliteit tussen alle typen van client en server.</span><span class="sxs-lookup"><span data-stu-id="6dc04-124">The chart below shows the compatibility between all client and server types.</span></span> <span data-ttu-id="6dc04-125">Een back-end is geclassificeerd als beide Mobile **Services** of Mobile **Apps** op basis van de server-SDK die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6dc04-125">A backend is classified as either Mobile **Services** or Mobile **Apps** based on the server SDK that it uses.</span></span>

|  | <span data-ttu-id="6dc04-126">**Mobile Services** Node.js- of .NET</span><span class="sxs-lookup"><span data-stu-id="6dc04-126">**Mobile Services** Node.js or .NET</span></span> | <span data-ttu-id="6dc04-127">**Mobiele Apps** Node.js- of .NET</span><span class="sxs-lookup"><span data-stu-id="6dc04-127">**Mobile Apps** Node.js or .NET</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dc04-128">[Mobile Services-clients]</span><span class="sxs-lookup"><span data-stu-id="6dc04-128">[Mobile Services clients]</span></span> |<span data-ttu-id="6dc04-129">OK</span><span class="sxs-lookup"><span data-stu-id="6dc04-129">Ok</span></span> |<span data-ttu-id="6dc04-130">Fout\*</span><span class="sxs-lookup"><span data-stu-id="6dc04-130">Error\*</span></span> |
| <span data-ttu-id="6dc04-131">[Clients voor mobiele Apps]</span><span class="sxs-lookup"><span data-stu-id="6dc04-131">[Mobile Apps clients]</span></span> |<span data-ttu-id="6dc04-132">Fout\*</span><span class="sxs-lookup"><span data-stu-id="6dc04-132">Error\*</span></span> |<span data-ttu-id="6dc04-133">OK</span><span class="sxs-lookup"><span data-stu-id="6dc04-133">Ok</span></span> |

<span data-ttu-id="6dc04-134">\*Dit kan worden beheerd door te geven **MS_SkipVersionCheck**.</span><span class="sxs-lookup"><span data-stu-id="6dc04-134">\*This can be controlled by specifying **MS_SkipVersionCheck**.</span></span>

<!-- IMPORTANT!  The anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: the fwlink to this document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <span data-ttu-id="6dc04-135"><a name="1.0.0"></a>Mobile Services-client en server</span><span class="sxs-lookup"><span data-stu-id="6dc04-135"><a name="1.0.0"></a>Mobile Services client and server</span></span>
<span data-ttu-id="6dc04-136">De client-SDK's in de onderstaande tabel compatibel zijn met **Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="6dc04-136">The client SDKs in the table below are compatible with **Mobile Services**.</span></span>

<span data-ttu-id="6dc04-137">Opmerking: de Mobile Services-client SDK's *niet* een headerwaarde verzenden voor `ZUMO-API-VERSION`.</span><span class="sxs-lookup"><span data-stu-id="6dc04-137">Note: the Mobile Services client SDKs *do not* send a header value for `ZUMO-API-VERSION`.</span></span> <span data-ttu-id="6dc04-138">Als de service deze kop- of queryreekswaarde ontvangt, een fout geretourneerd, tenzij u expliciet uit zoals hierboven beschreven hebt gekozen.</span><span class="sxs-lookup"><span data-stu-id="6dc04-138">If the service receives this header or query string value, an error will be returned, unless you have explicitly opted out as described above.</span></span>

### <span data-ttu-id="6dc04-139"><a name="MobileServicesClients"></a>Mobiele *Services* client-SDK's</span><span class="sxs-lookup"><span data-stu-id="6dc04-139"><a name="MobileServicesClients"></a> Mobile *Services* client SDKs</span></span>
| <span data-ttu-id="6dc04-140">Clientplatform</span><span class="sxs-lookup"><span data-stu-id="6dc04-140">Client platform</span></span> | <span data-ttu-id="6dc04-141">Versie</span><span class="sxs-lookup"><span data-stu-id="6dc04-141">Version</span></span> | <span data-ttu-id="6dc04-142">De versieheaderwaarde</span><span class="sxs-lookup"><span data-stu-id="6dc04-142">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dc04-143">Beheerde client (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="6dc04-143">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="6dc04-144">1.3.2</span><span class="sxs-lookup"><span data-stu-id="6dc04-144">1.3.2</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |<span data-ttu-id="6dc04-145">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="6dc04-145">n/a</span></span> |
| <span data-ttu-id="6dc04-146">iOS</span><span class="sxs-lookup"><span data-stu-id="6dc04-146">iOS</span></span> |[<span data-ttu-id="6dc04-147">2.2.2</span><span class="sxs-lookup"><span data-stu-id="6dc04-147">2.2.2</span></span>](http://aka.ms/gc6fex) |<span data-ttu-id="6dc04-148">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="6dc04-148">n/a</span></span> |
| <span data-ttu-id="6dc04-149">Android</span><span class="sxs-lookup"><span data-stu-id="6dc04-149">Android</span></span> |[<span data-ttu-id="6dc04-150">2.0.3</span><span class="sxs-lookup"><span data-stu-id="6dc04-150">2.0.3</span></span>](https://go.microsoft.com/fwLink/?LinkID=280126) |<span data-ttu-id="6dc04-151">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="6dc04-151">n/a</span></span> |
| <span data-ttu-id="6dc04-152">HTML</span><span class="sxs-lookup"><span data-stu-id="6dc04-152">HTML</span></span> |[<span data-ttu-id="6dc04-153">1.2.7</span><span class="sxs-lookup"><span data-stu-id="6dc04-153">1.2.7</span></span>](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |<span data-ttu-id="6dc04-154">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="6dc04-154">n/a</span></span> |

### <a name="mobile-services-server-sdks"></a><span data-ttu-id="6dc04-155">Mobiele *Services* server SDK's</span><span class="sxs-lookup"><span data-stu-id="6dc04-155">Mobile *Services* server SDKs</span></span>
| <span data-ttu-id="6dc04-156">Server-platform</span><span class="sxs-lookup"><span data-stu-id="6dc04-156">Server platform</span></span> | <span data-ttu-id="6dc04-157">Versie</span><span class="sxs-lookup"><span data-stu-id="6dc04-157">Version</span></span> | <span data-ttu-id="6dc04-158">Geaccepteerde versie-header</span><span class="sxs-lookup"><span data-stu-id="6dc04-158">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dc04-159">.NET</span><span class="sxs-lookup"><span data-stu-id="6dc04-159">.NET</span></span> |[<span data-ttu-id="6dc04-160">WindowsAzure.MobileServices.Backend.* versie 1.0.x</span><span class="sxs-lookup"><span data-stu-id="6dc04-160">WindowsAzure.MobileServices.Backend.* Version 1.0.x</span></span>](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |<span data-ttu-id="6dc04-161">** Geen versiekop **</span><span class="sxs-lookup"><span data-stu-id="6dc04-161">**No version header **</span></span> |
| <span data-ttu-id="6dc04-162">Node.js</span><span class="sxs-lookup"><span data-stu-id="6dc04-162">Node.js</span></span> |<span data-ttu-id="6dc04-163">(binnenkort)</span><span class="sxs-lookup"><span data-stu-id="6dc04-163">(coming soon)</span></span> |<span data-ttu-id="6dc04-164">**Er is geen versie-header**</span><span class="sxs-lookup"><span data-stu-id="6dc04-164">**No version header**</span></span> |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a><span data-ttu-id="6dc04-165">Gedrag van de back-ends voor Mobile Services</span><span class="sxs-lookup"><span data-stu-id="6dc04-165">Behavior of Mobile Services backends</span></span>
| <span data-ttu-id="6dc04-166">ZUMO-API-VERSIE</span><span class="sxs-lookup"><span data-stu-id="6dc04-166">ZUMO-API-VERSION</span></span> | <span data-ttu-id="6dc04-167">Waarde van MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="6dc04-167">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="6dc04-168">Antwoord</span><span class="sxs-lookup"><span data-stu-id="6dc04-168">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dc04-169">Niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="6dc04-169">Not specified</span></span> |<span data-ttu-id="6dc04-170">Alle</span><span class="sxs-lookup"><span data-stu-id="6dc04-170">Any</span></span> |<span data-ttu-id="6dc04-171">200 - OK</span><span class="sxs-lookup"><span data-stu-id="6dc04-171">200 - OK</span></span> |
| <span data-ttu-id="6dc04-172">Een willekeurige waarde</span><span class="sxs-lookup"><span data-stu-id="6dc04-172">Any value</span></span> |<span data-ttu-id="6dc04-173">True</span><span class="sxs-lookup"><span data-stu-id="6dc04-173">True</span></span> |<span data-ttu-id="6dc04-174">200 - OK</span><span class="sxs-lookup"><span data-stu-id="6dc04-174">200 - OK</span></span> |
| <span data-ttu-id="6dc04-175">Een willekeurige waarde</span><span class="sxs-lookup"><span data-stu-id="6dc04-175">Any value</span></span> |<span data-ttu-id="6dc04-176">ONWAAR/niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="6dc04-176">False/Not Specified</span></span> |<span data-ttu-id="6dc04-177">400 - onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="6dc04-177">400 - Bad Request</span></span> |

## <span data-ttu-id="6dc04-178"><a name="2.0.0"></a>Azure Mobile Apps-client en server</span><span class="sxs-lookup"><span data-stu-id="6dc04-178"><a name="2.0.0"></a>Azure Mobile Apps client and server</span></span>
### <span data-ttu-id="6dc04-179"><a name="MobileAppsClients"></a>Mobiele *Apps* client-SDK's</span><span class="sxs-lookup"><span data-stu-id="6dc04-179"><a name="MobileAppsClients"></a> Mobile *Apps* client SDKs</span></span>
<span data-ttu-id="6dc04-180">Beginnen met de volgende versies van de client-SDK versiecontrole is geïntroduceerd voor **Azure Mobile Apps**:</span><span class="sxs-lookup"><span data-stu-id="6dc04-180">Version checking was introduced starting with the following versions of the client SDK for **Azure Mobile Apps**:</span></span>

| <span data-ttu-id="6dc04-181">Clientplatform</span><span class="sxs-lookup"><span data-stu-id="6dc04-181">Client platform</span></span> | <span data-ttu-id="6dc04-182">Versie</span><span class="sxs-lookup"><span data-stu-id="6dc04-182">Version</span></span> | <span data-ttu-id="6dc04-183">De versieheaderwaarde</span><span class="sxs-lookup"><span data-stu-id="6dc04-183">Version header value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dc04-184">Beheerde client (Windows, Xamarin)</span><span class="sxs-lookup"><span data-stu-id="6dc04-184">Managed client (Windows, Xamarin)</span></span> |[<span data-ttu-id="6dc04-185">2.0.0</span><span class="sxs-lookup"><span data-stu-id="6dc04-185">2.0.0</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |<span data-ttu-id="6dc04-186">2.0.0</span><span class="sxs-lookup"><span data-stu-id="6dc04-186">2.0.0</span></span> |
| <span data-ttu-id="6dc04-187">iOS</span><span class="sxs-lookup"><span data-stu-id="6dc04-187">iOS</span></span> |[<span data-ttu-id="6dc04-188">3.0.0</span><span class="sxs-lookup"><span data-stu-id="6dc04-188">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=529823) |<span data-ttu-id="6dc04-189">2.0.0</span><span class="sxs-lookup"><span data-stu-id="6dc04-189">2.0.0</span></span> |
| <span data-ttu-id="6dc04-190">Android</span><span class="sxs-lookup"><span data-stu-id="6dc04-190">Android</span></span> |[<span data-ttu-id="6dc04-191">3.0.0</span><span class="sxs-lookup"><span data-stu-id="6dc04-191">3.0.0</span></span>](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |<span data-ttu-id="6dc04-192">3.0.0</span><span class="sxs-lookup"><span data-stu-id="6dc04-192">3.0.0</span></span> |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a><span data-ttu-id="6dc04-193">Mobiele *Apps* server SDK's</span><span class="sxs-lookup"><span data-stu-id="6dc04-193">Mobile *Apps* server SDKs</span></span>
<span data-ttu-id="6dc04-194">Versiecontrole is opgenomen in de volgende server SDK-versies:</span><span class="sxs-lookup"><span data-stu-id="6dc04-194">Version checking is included in following server SDK versions:</span></span>

| <span data-ttu-id="6dc04-195">Server-platform</span><span class="sxs-lookup"><span data-stu-id="6dc04-195">Server platform</span></span> | <span data-ttu-id="6dc04-196">SDK</span><span class="sxs-lookup"><span data-stu-id="6dc04-196">SDK</span></span> | <span data-ttu-id="6dc04-197">Geaccepteerde versie-header</span><span class="sxs-lookup"><span data-stu-id="6dc04-197">Accepted version header</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dc04-198">.NET</span><span class="sxs-lookup"><span data-stu-id="6dc04-198">.NET</span></span> |[<span data-ttu-id="6dc04-199">Microsoft.Azure.Mobile.Server</span><span class="sxs-lookup"><span data-stu-id="6dc04-199">Microsoft.Azure.Mobile.Server</span></span>](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |<span data-ttu-id="6dc04-200">2.0.0</span><span class="sxs-lookup"><span data-stu-id="6dc04-200">2.0.0</span></span> |
| <span data-ttu-id="6dc04-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="6dc04-201">Node.js</span></span> |[<span data-ttu-id="6dc04-202">Azure mobile apps)</span><span class="sxs-lookup"><span data-stu-id="6dc04-202">azure-mobile-apps)</span></span>](https://www.npmjs.com/package/azure-mobile-apps) |<span data-ttu-id="6dc04-203">2.0.0</span><span class="sxs-lookup"><span data-stu-id="6dc04-203">2.0.0</span></span> |

### <a name="behavior-of-mobile-apps-backends"></a><span data-ttu-id="6dc04-204">Gedrag van de back-ends voor mobiele Apps</span><span class="sxs-lookup"><span data-stu-id="6dc04-204">Behavior of Mobile Apps backends</span></span>
| <span data-ttu-id="6dc04-205">ZUMO-API-VERSIE</span><span class="sxs-lookup"><span data-stu-id="6dc04-205">ZUMO-API-VERSION</span></span> | <span data-ttu-id="6dc04-206">Waarde van MS_SkipVersionCheck</span><span class="sxs-lookup"><span data-stu-id="6dc04-206">Value of MS_SkipVersionCheck</span></span> | <span data-ttu-id="6dc04-207">Antwoord</span><span class="sxs-lookup"><span data-stu-id="6dc04-207">Response</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6dc04-208">x.y.z of Null zijn</span><span class="sxs-lookup"><span data-stu-id="6dc04-208">x.y.z or Null</span></span> |<span data-ttu-id="6dc04-209">True</span><span class="sxs-lookup"><span data-stu-id="6dc04-209">True</span></span> |<span data-ttu-id="6dc04-210">200 - OK</span><span class="sxs-lookup"><span data-stu-id="6dc04-210">200 - OK</span></span> |
| <span data-ttu-id="6dc04-211">Null</span><span class="sxs-lookup"><span data-stu-id="6dc04-211">Null</span></span> |<span data-ttu-id="6dc04-212">ONWAAR/niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="6dc04-212">False/Not Specified</span></span> |<span data-ttu-id="6dc04-213">400 - onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="6dc04-213">400 - Bad Request</span></span> |
| <span data-ttu-id="6dc04-214">1.x.y</span><span class="sxs-lookup"><span data-stu-id="6dc04-214">1.x.y</span></span> |<span data-ttu-id="6dc04-215">ONWAAR/niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="6dc04-215">False/Not Specified</span></span> |<span data-ttu-id="6dc04-216">400 - onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="6dc04-216">400 - Bad Request</span></span> |
| <span data-ttu-id="6dc04-217">2.0.0-2.x.y</span><span class="sxs-lookup"><span data-stu-id="6dc04-217">2.0.0-2.x.y</span></span> |<span data-ttu-id="6dc04-218">ONWAAR/niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="6dc04-218">False/Not Specified</span></span> |<span data-ttu-id="6dc04-219">200 - OK</span><span class="sxs-lookup"><span data-stu-id="6dc04-219">200 - OK</span></span> |
| <span data-ttu-id="6dc04-220">3.0.0-3.x.y</span><span class="sxs-lookup"><span data-stu-id="6dc04-220">3.0.0-3.x.y</span></span> |<span data-ttu-id="6dc04-221">ONWAAR/niet opgegeven</span><span class="sxs-lookup"><span data-stu-id="6dc04-221">False/Not Specified</span></span> |<span data-ttu-id="6dc04-222">400 - onjuiste aanvraag</span><span class="sxs-lookup"><span data-stu-id="6dc04-222">400 - Bad Request</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6dc04-223">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6dc04-223">Next Steps</span></span>
* <span data-ttu-id="6dc04-224">[een mobiele Service migreren naar Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="6dc04-224">[Migrate a Mobile Service to Azure App Service]</span></span>

<span data-ttu-id="6dc04-225">[Mobile Services-clients]: #MobileServicesClients</span><span class="sxs-lookup"><span data-stu-id="6dc04-225">[Mobile Services clients]: #MobileServicesClients</span></span>
<span data-ttu-id="6dc04-226">[Clients voor mobiele Apps]: #MobileAppsClients</span><span class="sxs-lookup"><span data-stu-id="6dc04-226">[Mobile Apps clients]: #MobileAppsClients</span></span>


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
<span data-ttu-id="6dc04-227">[een mobiele Service migreren naar Azure App Service]: app-service-mobile-migrating-from-mobile-services.md</span><span class="sxs-lookup"><span data-stu-id="6dc04-227">[Migrate a Mobile Service to Azure App Service]: app-service-mobile-migrating-from-mobile-services.md</span></span>

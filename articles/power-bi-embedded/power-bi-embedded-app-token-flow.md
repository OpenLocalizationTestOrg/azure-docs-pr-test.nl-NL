---
title: aaaAuthenticating en autoriseren met Power BI Embedded
description: "Verifiëren en autoriseren met Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 1c1369ea-7dfd-4b6e-978b-8f78908fd6f6
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 483ca0499e8d03584e1151d3d278c0179d4b8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticating-and-authorizing-with-power-bi-embedded"></a><span data-ttu-id="bee98-103">Verifiëren en autoriseren met Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="bee98-103">Authenticating and authorizing with Power BI Embedded</span></span>

<span data-ttu-id="bee98-104">maakt gebruik van Power BI Embedded service Hallo **sleutels** en **App-Tokens** voor verificatie en autorisatie in plaats van expliciete eindgebruiker verificatie.</span><span class="sxs-lookup"><span data-stu-id="bee98-104">hello Power BI Embedded service uses **Keys** and **App Tokens** for authentication and authorization, instead of explicit end-user authentication.</span></span> <span data-ttu-id="bee98-105">In dit model wordt beheerd door uw toepassing verificatie en autorisatie voor uw eindgebruikers.</span><span class="sxs-lookup"><span data-stu-id="bee98-105">In this model, your application manages authentication and authorization for your end-users.</span></span> <span data-ttu-id="bee98-106">Indien nodig, wordt uw app maakt en stuurt Hallo App-Tokens die onze service toorender vertelt Hallo gevraagde rapport.</span><span class="sxs-lookup"><span data-stu-id="bee98-106">When necessary, your app creates and sends hello App Tokens that tells our service toorender hello requested report.</span></span> <span data-ttu-id="bee98-107">Dit ontwerp nodig uw app toouse Azure Active Directory niet voor verificatie en autorisatie, hoewel u nog steeds kunt.</span><span class="sxs-lookup"><span data-stu-id="bee98-107">This design doesn't require your app toouse Azure Active Directory for user authentication and authorization, although you still can.</span></span>

## <a name="two-ways-tooauthenticate"></a><span data-ttu-id="bee98-108">Twee manieren tooauthenticate</span><span class="sxs-lookup"><span data-stu-id="bee98-108">Two ways tooauthenticate</span></span>

<span data-ttu-id="bee98-109">**Sleutel** -kunt u sleutels gebruiken voor alle Power BI Embedded REST API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="bee98-109">**Key** -  You can use keys for all Power BI Embedded REST API calls.</span></span> <span data-ttu-id="bee98-110">Hallo-codes kunnen u vinden in Hallo **Azure-portal** door te klikken op **alle instellingen** en vervolgens **toegangssleutels**.</span><span class="sxs-lookup"><span data-stu-id="bee98-110">hello keys can be found in hello **Azure portal** by clicking on **All settings** and then **Access keys**.</span></span> <span data-ttu-id="bee98-111">Uw sleutel altijd behandeld alsof het een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="bee98-111">Always treat your key as if it were a password.</span></span> <span data-ttu-id="bee98-112">Deze sleutels ook machtigingen toomake REST API niet aanroepen voor een bepaalde werkruimte-verzameling.</span><span class="sxs-lookup"><span data-stu-id="bee98-112">These keys have permissions toomake any REST API call on a particular workspace collection.</span></span>

<span data-ttu-id="bee98-113">een sleutel op een REST-aanroep toouse Hallo na autorisatie-header toevoegen:</span><span class="sxs-lookup"><span data-stu-id="bee98-113">toouse a key on a REST call, add hello following authorization header:</span></span>            

    Authorization: AppKey {your key}

<span data-ttu-id="bee98-114">**App-token** -App-tokens worden gebruikt voor alle insluiten aanvragen.</span><span class="sxs-lookup"><span data-stu-id="bee98-114">**App token** - App tokens are used for all embedding requests.</span></span> <span data-ttu-id="bee98-115">Ze zijn ontworpen toobe uitvoeren clientzijde, zodat ze beperkte tooa één rapport en de best practice tooset een verlooptijd.</span><span class="sxs-lookup"><span data-stu-id="bee98-115">They’re designed toobe run client-side, so they're restricted tooa single report and it’s best practice tooset an expiration time.</span></span>

<span data-ttu-id="bee98-116">App-tokens zijn een JWT (JSON Web Token) die is ondertekend door een van uw sleutels.</span><span class="sxs-lookup"><span data-stu-id="bee98-116">App tokens are a JWT (JSON Web Token) that is signed by one of your keys.</span></span>

<span data-ttu-id="bee98-117">Uw app-token kan Hallo claims volgende bevatten:</span><span class="sxs-lookup"><span data-stu-id="bee98-117">Your app token can contain hello following claims:</span></span>

| <span data-ttu-id="bee98-118">Claim</span><span class="sxs-lookup"><span data-stu-id="bee98-118">Claim</span></span> | <span data-ttu-id="bee98-119">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bee98-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bee98-120">**ver**</span><span class="sxs-lookup"><span data-stu-id="bee98-120">**ver**</span></span> |<span data-ttu-id="bee98-121">Hallo-versie van Hallo app-token.</span><span class="sxs-lookup"><span data-stu-id="bee98-121">hello version of hello app token.</span></span> <span data-ttu-id="bee98-122">0.2.0 is Hallo huidige versie.</span><span class="sxs-lookup"><span data-stu-id="bee98-122">0.2.0 is hello current version.</span></span> |
| <span data-ttu-id="bee98-123">**AUD**</span><span class="sxs-lookup"><span data-stu-id="bee98-123">**aud**</span></span> |<span data-ttu-id="bee98-124">Hallo bedoeld ontvanger van Hallo-token.</span><span class="sxs-lookup"><span data-stu-id="bee98-124">hello intended recipient of hello token.</span></span> <span data-ttu-id="bee98-125">Voor Power BI Embedded gebruik: 'https://analysis.windows.net/powerbi/api'.</span><span class="sxs-lookup"><span data-stu-id="bee98-125">For Power BI Embedded use: “https://analysis.windows.net/powerbi/api”.</span></span> |
| <span data-ttu-id="bee98-126">**ISS**</span><span class="sxs-lookup"><span data-stu-id="bee98-126">**iss**</span></span> |<span data-ttu-id="bee98-127">Een tekenreeks die aangeeft Hallo toepassing hello token uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="bee98-127">A string indicating hello application which issued hello token.</span></span> |
| <span data-ttu-id="bee98-128">**type**</span><span class="sxs-lookup"><span data-stu-id="bee98-128">**type**</span></span> |<span data-ttu-id="bee98-129">Hallo-type van app-token dat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bee98-129">hello type of app token which is being created.</span></span> <span data-ttu-id="bee98-130">Huidige Hallo alleen ondersteund type is **insluiten**.</span><span class="sxs-lookup"><span data-stu-id="bee98-130">Current hello only supported type is **embed**.</span></span> |
| <span data-ttu-id="bee98-131">**draadloze**</span><span class="sxs-lookup"><span data-stu-id="bee98-131">**wcn**</span></span> |<span data-ttu-id="bee98-132">Werkruimte verzameling naam Hallo token wordt uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="bee98-132">Workspace collection name hello token is being issued for.</span></span> |
| <span data-ttu-id="bee98-133">**WID**</span><span class="sxs-lookup"><span data-stu-id="bee98-133">**wid**</span></span> |<span data-ttu-id="bee98-134">Werkruimte-ID Hallo token wordt uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="bee98-134">Workspace ID hello token is being issued for.</span></span> |
| <span data-ttu-id="bee98-135">**RID**</span><span class="sxs-lookup"><span data-stu-id="bee98-135">**rid**</span></span> |<span data-ttu-id="bee98-136">Rapport ID Hallo token wordt uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="bee98-136">Report ID hello token is being issued for.</span></span> |
| <span data-ttu-id="bee98-137">**gebruikersnaam** (optioneel)</span><span class="sxs-lookup"><span data-stu-id="bee98-137">**username** (optional)</span></span> |<span data-ttu-id="bee98-138">Gebruikt voor beveiliging op Rijniveau, is dit een tekenreeks waarmee Hallo gebruiker identificeren wanneer RLS regels toepassen.</span><span class="sxs-lookup"><span data-stu-id="bee98-138">Used with RLS, this is a string that can help identify hello user when applying RLS rules.</span></span> |
| <span data-ttu-id="bee98-139">**rollen** (optioneel)</span><span class="sxs-lookup"><span data-stu-id="bee98-139">**roles** (optional)</span></span> |<span data-ttu-id="bee98-140">Een tekenreeks met Hallo rollen tooselect bij het toepassen van regels voor beveiliging op rijniveau.</span><span class="sxs-lookup"><span data-stu-id="bee98-140">A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="bee98-141">Als meer dan één rol wordt doorgegeven, moeten worden doorgegeven als een String-matrix.</span><span class="sxs-lookup"><span data-stu-id="bee98-141">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="bee98-142">**SCP** (optioneel)</span><span class="sxs-lookup"><span data-stu-id="bee98-142">**scp** (optional)</span></span> |<span data-ttu-id="bee98-143">Een tekenreeks met Hallo machtigingen scopes.</span><span class="sxs-lookup"><span data-stu-id="bee98-143">A string containing hello permissions scopes.</span></span> <span data-ttu-id="bee98-144">Als meer dan één rol wordt doorgegeven, moeten worden doorgegeven als een String-matrix.</span><span class="sxs-lookup"><span data-stu-id="bee98-144">If passing more than one role, they should be passed as a sting array.</span></span> |
| <span data-ttu-id="bee98-145">**EXP** (optioneel)</span><span class="sxs-lookup"><span data-stu-id="bee98-145">**exp** (optional)</span></span> |<span data-ttu-id="bee98-146">Hiermee wordt aangegeven in welke Hallo-token verloopt Hallo-tijd.</span><span class="sxs-lookup"><span data-stu-id="bee98-146">Indicates hello time in which hello token will expire.</span></span> <span data-ttu-id="bee98-147">Deze moeten worden doorgegeven als Unix tijdstempels.</span><span class="sxs-lookup"><span data-stu-id="bee98-147">These should be passed in as Unix timestamps.</span></span> |
| <span data-ttu-id="bee98-148">**NBF** (optioneel)</span><span class="sxs-lookup"><span data-stu-id="bee98-148">**nbf** (optional)</span></span> |<span data-ttu-id="bee98-149">Geeft aan in welke Hallo token begint geldig Hallo-tijd.</span><span class="sxs-lookup"><span data-stu-id="bee98-149">Indicates hello time in which hello token starts being valid.</span></span> <span data-ttu-id="bee98-150">Deze moeten worden doorgegeven als Unix tijdstempels.</span><span class="sxs-lookup"><span data-stu-id="bee98-150">These should be passed in as Unix timestamps.</span></span> |

<span data-ttu-id="bee98-151">Een voorbeeld-app-token ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="bee98-151">A sample app token will look like this:</span></span>

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ2ZXIiOiIwLjIuMCIsInR5cGUiOiJlbWJlZCIsIndjbiI6Ikd1eUluQUN1YmUiLCJ3aWQiOiJkNGZlMWViMS0yNzEwLTRhNDctODQ3Yy0xNzZhOTU0NWRhZDgiLCJyaWQiOiIyNWMwZDQwYi1kZTY1LTQxZDItOTMyYy0wZjE2ODc2ZTNiOWQiLCJzY3AiOiJSZXBvcnQuUmVhZCIsImlzcyI6IlBvd2VyQklTREsiLCJhdWQiOiJodHRwczovL2FuYWx5c2lzLndpbmRvd3MubmV0L3Bvd2VyYmkvYXBpIiwiZXhwIjoxNDg4NTAyNDM2LCJuYmYiOjE0ODg0OTg4MzZ9.v1znUaXMrD1AdMz6YjywhJQGY7MWjdCR3SmUSwWwIiI
```

<span data-ttu-id="bee98-152">Wanneer gedecodeerd, deze wordt als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="bee98-152">When decoded, it will look something like this:</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

<span data-ttu-id="bee98-153">Er zijn methoden beschikbaar binnen Hallo SDK's die het maken van apptokens te vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="bee98-153">There are methods available within hello SDKs that make creation of apptokens easier.</span></span> <span data-ttu-id="bee98-154">Bijvoorbeeld: voor .NET u kunt bekijkt hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) klasse en Hallo [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methoden.</span><span class="sxs-lookup"><span data-stu-id="bee98-154">For example, for .NET you can look at hello [Microsoft.PowerBI.Security.PowerBIToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken) class and hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_) methods.</span></span>

<span data-ttu-id="bee98-155">Voor de .NET SDK hello, raadpleegt u te[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span><span class="sxs-lookup"><span data-stu-id="bee98-155">For hello .NET SDK, you can refer too[Scopes](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.scopes).</span></span>

## <a name="scopes"></a><span data-ttu-id="bee98-156">Scopes</span><span class="sxs-lookup"><span data-stu-id="bee98-156">Scopes</span></span>

<span data-ttu-id="bee98-157">Wanneer u insluiten tokens gebruikt, kunt u toorestrict informatie over het gebruik van Hallo-resources die u toegang te geven.</span><span class="sxs-lookup"><span data-stu-id="bee98-157">When using Embed tokens, you may want toorestrict usage of hello resources you give access to.</span></span> <span data-ttu-id="bee98-158">Daarom kunt u een token met bereik machtigingen genereren.</span><span class="sxs-lookup"><span data-stu-id="bee98-158">For this reason, you can generate a token with scoped permissions.</span></span>

<span data-ttu-id="bee98-159">Hallo volgen Hallo beschikbare scopes voor Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="bee98-159">hello following are hello available scopes for Power BI Embedded.</span></span>

|<span data-ttu-id="bee98-160">Bereik</span><span class="sxs-lookup"><span data-stu-id="bee98-160">Scope</span></span>|<span data-ttu-id="bee98-161">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bee98-161">Description</span></span>|
|---|---|
|<span data-ttu-id="bee98-162">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="bee98-162">Dataset.Read</span></span>|<span data-ttu-id="bee98-163">Machtigingsinstellingen tooread Hallo opgegeven gegevensset.</span><span class="sxs-lookup"><span data-stu-id="bee98-163">Provides permission tooread hello specified dataset.</span></span>|
|<span data-ttu-id="bee98-164">Dataset.Write</span><span class="sxs-lookup"><span data-stu-id="bee98-164">Dataset.Write</span></span>|<span data-ttu-id="bee98-165">Biedt machtiging toowrite toohello opgegeven gegevensset.</span><span class="sxs-lookup"><span data-stu-id="bee98-165">Provides permission toowrite toohello specified dataset.</span></span>|
|<span data-ttu-id="bee98-166">Dataset.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="bee98-166">Dataset.ReadWrite</span></span>|<span data-ttu-id="bee98-167">Machtiging tooread en write toohello samengesteld dataset biedt.</span><span class="sxs-lookup"><span data-stu-id="bee98-167">Provides permission tooread and write toohello specificed dataset.</span></span>|
|<span data-ttu-id="bee98-168">Report.Read</span><span class="sxs-lookup"><span data-stu-id="bee98-168">Report.Read</span></span>|<span data-ttu-id="bee98-169">Machtigingsinstellingen tooview Hallo opgegeven rapport.</span><span class="sxs-lookup"><span data-stu-id="bee98-169">Provides permission tooview hello specified report.</span></span>|
|<span data-ttu-id="bee98-170">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="bee98-170">Report.ReadWrite</span></span>|<span data-ttu-id="bee98-171">Biedt machtiging tooview en bewerk Hallo opgegeven rapport.</span><span class="sxs-lookup"><span data-stu-id="bee98-171">Provides permission tooview and edit hello specified report.</span></span>|
|<span data-ttu-id="bee98-172">Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="bee98-172">Workspace.Report.Create</span></span>|<span data-ttu-id="bee98-173">Machtiging toocreate biedt een nieuw rapport binnen Hallo opgegeven werkruimte.</span><span class="sxs-lookup"><span data-stu-id="bee98-173">Provides permission toocreate a new report within hello specified workspace.</span></span>|
|<span data-ttu-id="bee98-174">Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="bee98-174">Workspace.Report.Copy</span></span>|<span data-ttu-id="bee98-175">Machtiging tooclone biedt een bestaand rapport binnen Hallo opgegeven werkruimte.</span><span class="sxs-lookup"><span data-stu-id="bee98-175">Provides permission tooclone an existing report within hello specified workspace.</span></span>|

<span data-ttu-id="bee98-176">U kunt meerdere scopes opgeven met een spatie tussen Hallo scopes Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="bee98-176">You can supply multiple scopes by using a space between hello scopes like hello following.</span></span>

```
string scopes = "Dataset.Read Workspace.Report.Create";
```

<span data-ttu-id="bee98-177">**Vereiste claims - scopes**</span><span class="sxs-lookup"><span data-stu-id="bee98-177">**Required claims - scopes**</span></span>

<span data-ttu-id="bee98-178">SCP: {scopesClaim} scopesClaim mag een tekenreeks of een matrix van tekenreeksen, let Hallo toegestane machtigingen tooworkspace resources (rapport, gegevensset, enz.)</span><span class="sxs-lookup"><span data-stu-id="bee98-178">scp: {scopesClaim} scopesClaim can be either a string or array of strings, noting hello allowed permissions tooworkspace resources (Report, Dataset, etc.)</span></span>

<span data-ttu-id="bee98-179">Een gecodeerde token, met de scopes die zijn gedefinieerd, ziet er vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="bee98-179">A decoded token, with scopes defined, would look similar toohello following.</span></span>

```
Header

{
    typ: "JWT",
    alg: "HS256:
}

Body

{
  "ver": "0.2.0",
  "wcn": "SupportDemo",
  "wid": "ca675b19-6c3c-4003-8808-1c7ddc6bd809",
  "rid": "96241f0f-abae-4ea9-a065-93b428eddb17",
  "scp": "Report.Read",
  "iss": "PowerBISDK",
  "aud": "https://analysis.windows.net/powerbi/api",
  "exp": 1360047056,
  "nbf": 1360043456
}

```

### <a name="operations-and-scopes"></a><span data-ttu-id="bee98-180">Bewerkingen en -scopes</span><span class="sxs-lookup"><span data-stu-id="bee98-180">Operations and scopes</span></span>

|<span data-ttu-id="bee98-181">Bewerking</span><span class="sxs-lookup"><span data-stu-id="bee98-181">Operation</span></span>|<span data-ttu-id="bee98-182">Doelbron</span><span class="sxs-lookup"><span data-stu-id="bee98-182">Target resource</span></span>|<span data-ttu-id="bee98-183">Token machtigingen</span><span class="sxs-lookup"><span data-stu-id="bee98-183">Token permissions</span></span>|
|---|---|---|
|<span data-ttu-id="bee98-184">Een nieuw rapport op basis van een gegevensset voor (in het geheugen) maken.</span><span class="sxs-lookup"><span data-stu-id="bee98-184">Create (in-memory) a new report based on a dataset.</span></span>|<span data-ttu-id="bee98-185">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="bee98-185">Dataset</span></span>|<span data-ttu-id="bee98-186">Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="bee98-186">Dataset.Read</span></span>|
|<span data-ttu-id="bee98-187">(In het geheugen) Maak een nieuw rapport op basis van een gegevensset en Hallo rapport opslaan.</span><span class="sxs-lookup"><span data-stu-id="bee98-187">Create (in-memory) a new report based on a dataset and save hello report.</span></span>|<span data-ttu-id="bee98-188">Gegevensset</span><span class="sxs-lookup"><span data-stu-id="bee98-188">Dataset</span></span>|<span data-ttu-id="bee98-189">* Dataset.Read</span><span class="sxs-lookup"><span data-stu-id="bee98-189">* Dataset.Read</span></span><br><span data-ttu-id="bee98-190">* Workspace.Report.Create</span><span class="sxs-lookup"><span data-stu-id="bee98-190">* Workspace.Report.Create</span></span>|
|<span data-ttu-id="bee98-191">(In het geheugen) een bestaand rapport verkennen/bewerken en weergeven.</span><span class="sxs-lookup"><span data-stu-id="bee98-191">View and explore/edit (in-memory) an existing report.</span></span> <span data-ttu-id="bee98-192">Report.Read impliceert Dataset.Read.</span><span class="sxs-lookup"><span data-stu-id="bee98-192">Report.Read implies Dataset.Read.</span></span> <span data-ttu-id="bee98-193">Hierdoor kunnen geen machtigingen toosave bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="bee98-193">This will not allow permissions toosave edits.</span></span>|<span data-ttu-id="bee98-194">Rapport</span><span class="sxs-lookup"><span data-stu-id="bee98-194">Report</span></span>|<span data-ttu-id="bee98-195">Report.Read</span><span class="sxs-lookup"><span data-stu-id="bee98-195">Report.Read</span></span>|
|<span data-ttu-id="bee98-196">Bewerken en opslaan van een bestaand rapport.</span><span class="sxs-lookup"><span data-stu-id="bee98-196">Edit and save an existing report.</span></span>|<span data-ttu-id="bee98-197">Rapport</span><span class="sxs-lookup"><span data-stu-id="bee98-197">Report</span></span>|<span data-ttu-id="bee98-198">Report.ReadWrite</span><span class="sxs-lookup"><span data-stu-id="bee98-198">Report.ReadWrite</span></span>|
|<span data-ttu-id="bee98-199">Sla een kopie van een rapport (OpslaanAls).</span><span class="sxs-lookup"><span data-stu-id="bee98-199">Save a copy of a report (Save As).</span></span>|<span data-ttu-id="bee98-200">Rapport</span><span class="sxs-lookup"><span data-stu-id="bee98-200">Report</span></span>|<span data-ttu-id="bee98-201">* Report.Read</span><span class="sxs-lookup"><span data-stu-id="bee98-201">* Report.Read</span></span><br><span data-ttu-id="bee98-202">* Workspace.Report.Copy</span><span class="sxs-lookup"><span data-stu-id="bee98-202">* Workspace.Report.Copy</span></span>|

## <a name="heres-how-hello-flow-works"></a><span data-ttu-id="bee98-203">Hier wordt de werking van Hallo stroom</span><span class="sxs-lookup"><span data-stu-id="bee98-203">Here's how hello flow works</span></span>
1. <span data-ttu-id="bee98-204">Hallo-API-sleutels tooyour toepassing kopiëren.</span><span class="sxs-lookup"><span data-stu-id="bee98-204">Copy hello API keys tooyour application.</span></span> <span data-ttu-id="bee98-205">U kunt Hallo sleutels krijgen in **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="bee98-205">You can get hello keys in **Azure Portal**.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
2. <span data-ttu-id="bee98-206">Token een claim asserts en heeft een verlooptijd.</span><span class="sxs-lookup"><span data-stu-id="bee98-206">Token asserts a claim and has an expiration time.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-2.png)
3. <span data-ttu-id="bee98-207">Token opgehaald ondertekend met een API-sleutels voor toegang.</span><span class="sxs-lookup"><span data-stu-id="bee98-207">Token gets signed with an API access keys.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-3.png)
4. <span data-ttu-id="bee98-208">Gebruiker vraagt tooview een rapport.</span><span class="sxs-lookup"><span data-stu-id="bee98-208">User requests tooview a report.</span></span>
   
    ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-4.png)
5. <span data-ttu-id="bee98-209">Token is gevalideerd met een API-sleutels voor toegang.</span><span class="sxs-lookup"><span data-stu-id="bee98-209">Token is validated with an API access keys.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-5.png)
6. <span data-ttu-id="bee98-210">Power BI Embedded verzendt een rapport toouser.</span><span class="sxs-lookup"><span data-stu-id="bee98-210">Power BI Embedded sends a report toouser.</span></span>
   
   ![](media/powerbi-embedded-get-started-sample/power-bi-embedded-token-6.png)

<span data-ttu-id="bee98-211">Na **Power BI Embedded** verzendt de gebruiker van een rapport toohello Hallo gebruiker Hallo rapport in uw aangepaste app kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="bee98-211">After **Power BI Embedded** sends a report toohello user, hello user can view hello report in your custom app.</span></span> <span data-ttu-id="bee98-212">Bijvoorbeeld, als u hebt geïmporteerd Hallo [analyseren verkoop gegevens PBIX voorbeeld](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), Hallo voorbeeld-web-app eruit als volgt:</span><span class="sxs-lookup"><span data-stu-id="bee98-212">For example, if you imported hello [Analyzing Sales Data PBIX sample](http://download.microsoft.com/download/1/4/E/14EDED28-6C58-4055-A65C-23B4DA81C4DE/Analyzing_Sales_Data.pbix), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="see-also"></a><span data-ttu-id="bee98-213">Zie ook</span><span class="sxs-lookup"><span data-stu-id="bee98-213">See Also</span></span>

[<span data-ttu-id="bee98-214">CreateReportEmbedToken</span><span class="sxs-lookup"><span data-stu-id="bee98-214">CreateReportEmbedToken</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#methods_)  
[<span data-ttu-id="bee98-215">Aan de slag met Microsoft Power BI Embedded voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bee98-215">Get started with Microsoft Power BI Embedded sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="bee98-216">Algemene scenario's voor Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="bee98-216">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="bee98-217">Aan de slag met Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="bee98-217">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="bee98-218">Power BI-CSharp Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="bee98-218">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
<span data-ttu-id="bee98-219">Nog vragen?</span><span class="sxs-lookup"><span data-stu-id="bee98-219">More questions?</span></span> [<span data-ttu-id="bee98-220">Probeer Hallo Power BI-Community</span><span class="sxs-lookup"><span data-stu-id="bee98-220">Try hello Power BI Community</span></span>](http://community.powerbi.com/)


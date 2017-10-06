---
title: controle van de Active Directory aaaAzure API-referentiemateriaal | Microsoft Docs
description: Hoe tooget Hello audit-API van Azure Active Directory gestart
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="36a4d-103">Azure Active Directory-audit API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="36a4d-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="36a4d-104">In dit onderwerp maakt deel uit van een verzameling van onderwerpen over hello Azure Active Directory rapportage-API.</span><span class="sxs-lookup"><span data-stu-id="36a4d-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="36a4d-105">Rapportage van Azure AD biedt u een API waarmee u tooaccess controlegegevens met code of gerelateerde hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="36a4d-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="36a4d-106">Hallo-bereik van dit onderwerp is tooprovide u met naslaginformatie over Hallo **audit API**.</span><span class="sxs-lookup"><span data-stu-id="36a4d-106">hello scope of this topic is tooprovide you with reference information about hello **audit API**.</span></span>

<span data-ttu-id="36a4d-107">Zie:</span><span class="sxs-lookup"><span data-stu-id="36a4d-107">See:</span></span>

* <span data-ttu-id="36a4d-108">[Controlelogboeken](active-directory-reporting-azure-portal.md#activity-reports) voor meer conceptuele informatie</span><span class="sxs-lookup"><span data-stu-id="36a4d-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="36a4d-109">[Aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md) voor meer informatie over Hallo rapportage-API.</span><span class="sxs-lookup"><span data-stu-id="36a4d-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


<span data-ttu-id="36a4d-110">Voor:</span><span class="sxs-lookup"><span data-stu-id="36a4d-110">For:</span></span>

- <span data-ttu-id="36a4d-111">Veelgestelde vragen, Lees onze [Veelgestelde vragen](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="36a4d-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="36a4d-112">Uitgeeft, neem [een ondersteuningsticket bestand](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="36a4d-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-hello-data"></a><span data-ttu-id="36a4d-113">Wie toegang heeft tot Hallo gegevens?</span><span class="sxs-lookup"><span data-stu-id="36a4d-113">Who can access hello data?</span></span>
* <span data-ttu-id="36a4d-114">Gebruikers met de rol beheerder beveiliging of beveiliging Reader Hallo</span><span class="sxs-lookup"><span data-stu-id="36a4d-114">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="36a4d-115">Globale beheerders</span><span class="sxs-lookup"><span data-stu-id="36a4d-115">Global Admins</span></span>
* <span data-ttu-id="36a4d-116">Elke app die autorisatie tooaccess Hallo API is (app autorisatie worden instellingen slechts op basis van toestemming van de globale beheerder)</span><span class="sxs-lookup"><span data-stu-id="36a4d-116">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36a4d-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="36a4d-117">Prerequisites</span></span>
<span data-ttu-id="36a4d-118">In de volgorde tooaccess in deze lijst via Hallo rapportage-API, moet u hebben:</span><span class="sxs-lookup"><span data-stu-id="36a4d-118">In order tooaccess this report through hello Reporting API, you must have:</span></span>

* <span data-ttu-id="36a4d-119">Een [Azure Active Directory gratis of betere edition](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="36a4d-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="36a4d-120">Voltooide Hallo [vereisten tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="36a4d-120">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="36a4d-121">Toegang tot Hallo-API</span><span class="sxs-lookup"><span data-stu-id="36a4d-121">Accessing hello API</span></span>
<span data-ttu-id="36a4d-122">U kunt deze API voor installatie zonder toezicht benaderen via Hallo [grafiek Explorer](https://graphexplorer2.cloudapp.net) of programmatisch met bijvoorbeeld PowerShell.</span><span class="sxs-lookup"><span data-stu-id="36a4d-122">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="36a4d-123">In de volgorde voor PowerShell toocorrectly interpreteren Hallo OData-filtersyntaxis gebruikt in AAD grafiek REST-aanroepen, moet u Hallo backtick (aka: ernstig accent) teken te 'escape' hello $-teken.</span><span class="sxs-lookup"><span data-stu-id="36a4d-123">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="36a4d-124">Hallo backtick teken fungeert als [PowerShell van escape-teken](https://technet.microsoft.com/library/hh847755.aspx)PowerShell toodo zodat een letterlijke interpretatie van Hallo $-teken en te voorkomen dat deze als de naam van een PowerShell-variabele verwarrend (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="36a4d-124">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="36a4d-125">in dit onderwerp Hallo richt zich op Hallo grafiek Explorer.</span><span class="sxs-lookup"><span data-stu-id="36a4d-125">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="36a4d-126">Zie voor een voorbeeld van PowerShell [PowerShell-script](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="36a4d-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="36a4d-127">API-eindpunt</span><span class="sxs-lookup"><span data-stu-id="36a4d-127">API Endpoint</span></span>
<span data-ttu-id="36a4d-128">U kunt toegang tot deze API met behulp van Hallo URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="36a4d-128">You can access this API using hello following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="36a4d-129">Er is geen limiet voor het aantal records dat wordt geretourneerd door hello Azure AD audit-API (OData paginering met) Hallo.</span><span class="sxs-lookup"><span data-stu-id="36a4d-129">There is no limit on hello number of records returned by hello Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="36a4d-130">Bekijk voor ondergrenzen voor de bewaarperiode op rapportagegegevens [bewaarbeleidsregels Reporting](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="36a4d-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="36a4d-131">Deze aanroep retourneert Hallo gegevens in batches.</span><span class="sxs-lookup"><span data-stu-id="36a4d-131">This call returns hello data in batches.</span></span> <span data-ttu-id="36a4d-132">Elke batch heeft maximaal 1000 records.</span><span class="sxs-lookup"><span data-stu-id="36a4d-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="36a4d-133">tooget hello volgende batch van records, volgende Hallo-verbinding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="36a4d-133">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="36a4d-134">Hallo skiptoken informatie ophalen uit de eerste set Hallo van de geretourneerde records.</span><span class="sxs-lookup"><span data-stu-id="36a4d-134">Get hello skiptoken information from hello first set of returned records.</span></span> <span data-ttu-id="36a4d-135">Hallo skip-token worden achter Hallo Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="36a4d-135">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="36a4d-136">Ondersteunde filters</span><span class="sxs-lookup"><span data-stu-id="36a4d-136">Supported filters</span></span>
<span data-ttu-id="36a4d-137">U kunt kleiner Hallo aantal records dat wordt geretourneerd door een API-aanroep in de vorm van een filter.</span><span class="sxs-lookup"><span data-stu-id="36a4d-137">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="36a4d-138">Voor aanmelden API worden gerelateerde gegevens, Hallo na filters ondersteund:</span><span class="sxs-lookup"><span data-stu-id="36a4d-138">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="36a4d-139">**$top =\<aantal records toobe geretourneerd\>**  -toolimit Hallo aantal geretourneerde records.</span><span class="sxs-lookup"><span data-stu-id="36a4d-139">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="36a4d-140">Dit is een dure bewerking.</span><span class="sxs-lookup"><span data-stu-id="36a4d-140">This is an expensive operation.</span></span> <span data-ttu-id="36a4d-141">U moet dit filter niet gebruiken als u wilt dat tooreturn duizenden objecten.</span><span class="sxs-lookup"><span data-stu-id="36a4d-141">You should not use this filter if you want tooreturn thousands of objects.</span></span>     
* <span data-ttu-id="36a4d-142">**$filter =\<uw filterinstructie\>**  -toospecify op basis van ondersteunde filtervelden, registreert u het belangrijkst Hallo type Hallo</span><span class="sxs-lookup"><span data-stu-id="36a4d-142">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="36a4d-143">Ondersteunde filtervelden en -operators</span><span class="sxs-lookup"><span data-stu-id="36a4d-143">Supported filter fields and operators</span></span>
<span data-ttu-id="36a4d-144">toospecify hello type records die u belangrijk vindt, kunt u een filter-instructie die kan een bestand of een combinatie van Hallo na filtervelden bevatten:</span><span class="sxs-lookup"><span data-stu-id="36a4d-144">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="36a4d-145">[ActiviteitDatum](#activitydate) -definieert een datum of datumbereik</span><span class="sxs-lookup"><span data-stu-id="36a4d-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="36a4d-146">[categorie](#category) -Hallo categorie op het gewenste toofilter definieert.</span><span class="sxs-lookup"><span data-stu-id="36a4d-146">[category](#category) - defines hello category you want toofilter on.</span></span>
* <span data-ttu-id="36a4d-147">[activityStatus](#activitystatus) -definieert Hallo status van een activiteit</span><span class="sxs-lookup"><span data-stu-id="36a4d-147">[activityStatus](#activitystatus) - defines hello status of an activity</span></span>
* <span data-ttu-id="36a4d-148">[activityType](#activitytype) -definieert Hallo-type van een activiteit</span><span class="sxs-lookup"><span data-stu-id="36a4d-148">[activityType](#activitytype)  - defines hello type of an activity</span></span>
* <span data-ttu-id="36a4d-149">[activiteit](#activity) -Hallo activiteit definieert als tekenreeks</span><span class="sxs-lookup"><span data-stu-id="36a4d-149">[activity](#activity) - defines hello activity as string</span></span>  
* <span data-ttu-id="36a4d-150">[naam van deacteur/](#actorname) -Hallo actor definieert in de vorm van de naam van de Hallo acteur van</span><span class="sxs-lookup"><span data-stu-id="36a4d-150">[actor/name](#actorname) -   defines hello actor in form of hello actor's name</span></span>
* <span data-ttu-id="36a4d-151">[acteur/objectid](#actorobjectid) -Hallo actor definieert in de vorm van de Hallo actor-ID</span><span class="sxs-lookup"><span data-stu-id="36a4d-151">[actor/objectid](#actorobjectid) - defines hello actor in form of hello actor's ID</span></span>   
* <span data-ttu-id="36a4d-152">[acteur/upn](#actorupn) -Hallo actor definieert in de vorm van Hallo actor van principe (user Principal name)</span><span class="sxs-lookup"><span data-stu-id="36a4d-152">[actor/upn](#actorupn)  - defines hello actor in form of hello actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="36a4d-153">[doelnaam/](#targetname) -Hallo doel in de vorm van de naam van de Hallo acteur van definieert</span><span class="sxs-lookup"><span data-stu-id="36a4d-153">[target/name](#targetname)  - defines hello target in form of hello actor's name</span></span>
* <span data-ttu-id="36a4d-154">[doel/objectid](#targetobjectid) -Hallo doel definieert in de vorm van Hallo-doel-ID</span><span class="sxs-lookup"><span data-stu-id="36a4d-154">[target/objectid](#targetobjectid) - defines hello target in form of hello target's ID</span></span>  
* <span data-ttu-id="36a4d-155">[doel/upn](#targetupn) -Hallo actor definieert in de vorm van Hallo actor van principe (user Principal name)</span><span class="sxs-lookup"><span data-stu-id="36a4d-155">[target/upn](#targetupn) - defines hello actor in form of hello actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="36a4d-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="36a4d-156">activityDate</span></span>
<span data-ttu-id="36a4d-157">**Operators ondersteund**: eq, ge RP, gt, lt</span><span class="sxs-lookup"><span data-stu-id="36a4d-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="36a4d-158">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="36a4d-159">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-159">**Notes**:</span></span>

<span data-ttu-id="36a4d-160">DateTime-waarde moet in UTC-notatie</span><span class="sxs-lookup"><span data-stu-id="36a4d-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="36a4d-161">category</span><span class="sxs-lookup"><span data-stu-id="36a4d-161">category</span></span>

<span data-ttu-id="36a4d-162">**Ondersteunde waarden**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-162">**Supported values**:</span></span>

| <span data-ttu-id="36a4d-163">Category</span><span class="sxs-lookup"><span data-stu-id="36a4d-163">Category</span></span>                         | <span data-ttu-id="36a4d-164">Waarde</span><span class="sxs-lookup"><span data-stu-id="36a4d-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="36a4d-165">Hoofddirectory</span><span class="sxs-lookup"><span data-stu-id="36a4d-165">Core Directory</span></span>                   | <span data-ttu-id="36a4d-166">Directory</span><span class="sxs-lookup"><span data-stu-id="36a4d-166">Directory</span></span> |
| <span data-ttu-id="36a4d-167">Self-service voor wachtwoordbeheer</span><span class="sxs-lookup"><span data-stu-id="36a4d-167">Self-service Password Management</span></span> | <span data-ttu-id="36a4d-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="36a4d-168">SSPR</span></span>      |
| <span data-ttu-id="36a4d-169">Self-service voor groepsbeheer</span><span class="sxs-lookup"><span data-stu-id="36a4d-169">Self-service Group Management</span></span>    | <span data-ttu-id="36a4d-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="36a4d-170">SSGM</span></span>      |
| <span data-ttu-id="36a4d-171">Account inrichten</span><span class="sxs-lookup"><span data-stu-id="36a4d-171">Account Provisioning</span></span>             | <span data-ttu-id="36a4d-172">Sync</span><span class="sxs-lookup"><span data-stu-id="36a4d-172">Sync</span></span>      |
| <span data-ttu-id="36a4d-173">Automatische wachtwoordoverschakeling</span><span class="sxs-lookup"><span data-stu-id="36a4d-173">Automated Password Rollover</span></span>      | <span data-ttu-id="36a4d-174">Automatische wachtwoordoverschakeling</span><span class="sxs-lookup"><span data-stu-id="36a4d-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="36a4d-175">Identiteitsbeveiliging</span><span class="sxs-lookup"><span data-stu-id="36a4d-175">Identity Protection</span></span>              | <span data-ttu-id="36a4d-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="36a4d-176">IdentityProtection</span></span> |
| <span data-ttu-id="36a4d-177">Uitgenodigde gebruikers</span><span class="sxs-lookup"><span data-stu-id="36a4d-177">Invited Users</span></span>                    | <span data-ttu-id="36a4d-178">Uitgenodigde gebruikers</span><span class="sxs-lookup"><span data-stu-id="36a4d-178">Invited Users</span></span> |
| <span data-ttu-id="36a4d-179">MIM-service</span><span class="sxs-lookup"><span data-stu-id="36a4d-179">MIM Service</span></span>                      | <span data-ttu-id="36a4d-180">MIM-service</span><span class="sxs-lookup"><span data-stu-id="36a4d-180">MIM Service</span></span> |



<span data-ttu-id="36a4d-181">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="36a4d-181">**Supported operators**: eq</span></span>

<span data-ttu-id="36a4d-182">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="36a4d-183">ActivityStatus</span><span class="sxs-lookup"><span data-stu-id="36a4d-183">activityStatus</span></span>

<span data-ttu-id="36a4d-184">**Ondersteunde waarden**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-184">**Supported values**:</span></span>

| <span data-ttu-id="36a4d-185">Activiteitsstatus</span><span class="sxs-lookup"><span data-stu-id="36a4d-185">Activity Status</span></span> | <span data-ttu-id="36a4d-186">Waarde</span><span class="sxs-lookup"><span data-stu-id="36a4d-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="36a4d-187">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="36a4d-187">Success</span></span>         | <span data-ttu-id="36a4d-188">0</span><span class="sxs-lookup"><span data-stu-id="36a4d-188">0</span></span>     |
| <span data-ttu-id="36a4d-189">Fout</span><span class="sxs-lookup"><span data-stu-id="36a4d-189">Failure</span></span>         | <span data-ttu-id="36a4d-190">- 1</span><span class="sxs-lookup"><span data-stu-id="36a4d-190">- 1</span></span>   |

<span data-ttu-id="36a4d-191">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="36a4d-191">**Supported operators**: eq</span></span>

<span data-ttu-id="36a4d-192">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="36a4d-193">activityType</span><span class="sxs-lookup"><span data-stu-id="36a4d-193">activityType</span></span>
<span data-ttu-id="36a4d-194">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="36a4d-194">**Supported operators**: eq</span></span>

<span data-ttu-id="36a4d-195">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="36a4d-196">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-196">**Notes**:</span></span>

<span data-ttu-id="36a4d-197">hoofdlettergevoelig</span><span class="sxs-lookup"><span data-stu-id="36a4d-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="36a4d-198">Activiteit</span><span class="sxs-lookup"><span data-stu-id="36a4d-198">activity</span></span>
<span data-ttu-id="36a4d-199">**Operators ondersteund**: eq, bevat, startsWith</span><span class="sxs-lookup"><span data-stu-id="36a4d-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="36a4d-200">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="36a4d-201">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-201">**Notes**:</span></span>

<span data-ttu-id="36a4d-202">hoofdlettergevoelig</span><span class="sxs-lookup"><span data-stu-id="36a4d-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="36a4d-203">naam van de acteur /</span><span class="sxs-lookup"><span data-stu-id="36a4d-203">actor/name</span></span>
<span data-ttu-id="36a4d-204">**Operators ondersteund**: eq, bevat, startsWith</span><span class="sxs-lookup"><span data-stu-id="36a4d-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="36a4d-205">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="36a4d-206">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-206">**Notes**:</span></span>

<span data-ttu-id="36a4d-207">Niet-hoofdlettergevoelige</span><span class="sxs-lookup"><span data-stu-id="36a4d-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="36a4d-208">acteur/objectId</span><span class="sxs-lookup"><span data-stu-id="36a4d-208">actor/objectId</span></span>
<span data-ttu-id="36a4d-209">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="36a4d-209">**Supported operators**: eq</span></span>

<span data-ttu-id="36a4d-210">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="36a4d-211">doelnaam /</span><span class="sxs-lookup"><span data-stu-id="36a4d-211">target/name</span></span>
<span data-ttu-id="36a4d-212">**Operators ondersteund**: eq, bevat, startsWith</span><span class="sxs-lookup"><span data-stu-id="36a4d-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="36a4d-213">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="36a4d-214">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-214">**Notes**:</span></span>

<span data-ttu-id="36a4d-215">Niet-hoofdlettergevoelige</span><span class="sxs-lookup"><span data-stu-id="36a4d-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="36a4d-216">doel/upn</span><span class="sxs-lookup"><span data-stu-id="36a4d-216">target/upn</span></span>
<span data-ttu-id="36a4d-217">**Operators ondersteund**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="36a4d-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="36a4d-218">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="36a4d-219">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-219">**Notes**:</span></span>

* <span data-ttu-id="36a4d-220">Niet-hoofdlettergevoelige</span><span class="sxs-lookup"><span data-stu-id="36a4d-220">Case-insensitive</span></span>
* <span data-ttu-id="36a4d-221">U moet tooadd Hallo volledige naamruimte tijdens het opvragen van Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="36a4d-221">You need tooadd hello full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="36a4d-222">doel/objectId</span><span class="sxs-lookup"><span data-stu-id="36a4d-222">target/objectId</span></span>
<span data-ttu-id="36a4d-223">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="36a4d-223">**Supported operators**: eq</span></span>

<span data-ttu-id="36a4d-224">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="36a4d-225">acteur/upn</span><span class="sxs-lookup"><span data-stu-id="36a4d-225">actor/upn</span></span>
<span data-ttu-id="36a4d-226">**Operators ondersteund**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="36a4d-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="36a4d-227">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="36a4d-228">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="36a4d-228">**Notes**:</span></span>

* <span data-ttu-id="36a4d-229">Niet-hoofdlettergevoelige</span><span class="sxs-lookup"><span data-stu-id="36a4d-229">Case-insensitive</span></span> 
* <span data-ttu-id="36a4d-230">U moet tooadd Hallo volledige naamruimte tijdens het opvragen van Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="36a4d-230">You need tooadd hello full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="36a4d-231">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="36a4d-231">Next Steps</span></span>
* <span data-ttu-id="36a4d-232">Wilt u toosee voorbeelden voor gefilterde systeemactiviteiten?</span><span class="sxs-lookup"><span data-stu-id="36a4d-232">Do you want toosee examples for filtered system activities?</span></span> <span data-ttu-id="36a4d-233">Bekijk Hallo [voorbeelden van Azure Active Directory-audit API](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="36a4d-233">Check out hello [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="36a4d-234">Wilt u meer informatie over reporting hello Azure AD-API tooknow?</span><span class="sxs-lookup"><span data-stu-id="36a4d-234">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="36a4d-235">Zie [aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="36a4d-235">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>


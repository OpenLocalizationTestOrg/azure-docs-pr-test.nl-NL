---
title: Azure Active Directory-audit API-referentiemateriaal | Microsoft Docs
description: Hoe u aan de slag met de Azure Active Directory-audit-API
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
ms.openlocfilehash: 573e940c5390e7b990d889681eb37b73c5b253d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="bf1ff-103">Azure Active Directory-audit API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="bf1ff-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="bf1ff-104">In dit onderwerp maakt deel uit van een verzameling van onderwerpen over de Azure Active Directory rapportage-API.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="bf1ff-105">Rapportage van Azure AD biedt u een API waarmee u toegang krijgt tot controlegegevens met code of gerelateerde hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span></span>
<span data-ttu-id="bf1ff-106">Het bereik van dit onderwerp is om u te bieden informatie over de **audit API**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-106">The scope of this topic is to provide you with reference information about the **audit API**.</span></span>

<span data-ttu-id="bf1ff-107">Zie:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-107">See:</span></span>

* <span data-ttu-id="bf1ff-108">[Controlelogboeken](active-directory-reporting-azure-portal.md#activity-reports) voor meer conceptuele informatie</span><span class="sxs-lookup"><span data-stu-id="bf1ff-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="bf1ff-109">[Aan de slag met Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) voor meer informatie over de rapportage-API.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


<span data-ttu-id="bf1ff-110">Voor:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-110">For:</span></span>

- <span data-ttu-id="bf1ff-111">Veelgestelde vragen, Lees onze [Veelgestelde vragen](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="bf1ff-112">Uitgeeft, neem [een ondersteuningsticket bestand](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-the-data"></a><span data-ttu-id="bf1ff-113">Wie heeft er toegang tot de gegevens?</span><span class="sxs-lookup"><span data-stu-id="bf1ff-113">Who can access the data?</span></span>
* <span data-ttu-id="bf1ff-114">Gebruikers met de rol Beveiligingsbeheerder of Beveiligingslezer</span><span class="sxs-lookup"><span data-stu-id="bf1ff-114">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="bf1ff-115">Globale beheerders</span><span class="sxs-lookup"><span data-stu-id="bf1ff-115">Global Admins</span></span>
* <span data-ttu-id="bf1ff-116">Elke app die autorisatie is voor toegang tot de API (app autorisatie worden instellingen slechts op basis van toestemming van de globale beheerder)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-116">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf1ff-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bf1ff-117">Prerequisites</span></span>
<span data-ttu-id="bf1ff-118">Als u dit rapport opent via de rapportage-API, moet u het volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-118">In order to access this report through the Reporting API, you must have:</span></span>

* <span data-ttu-id="bf1ff-119">Een [Azure Active Directory gratis of betere edition](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="bf1ff-120">Voltooid de [vereisten voor toegang tot de Azure AD rapportage-API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-120">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="bf1ff-121">Toegang tot de API</span><span class="sxs-lookup"><span data-stu-id="bf1ff-121">Accessing the API</span></span>
<span data-ttu-id="bf1ff-122">U kunt de toegang tot deze API via de [grafiek Explorer](https://graphexplorer2.cloudapp.net) of programmatisch met bijvoorbeeld PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-122">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="bf1ff-123">In de volgorde voor PowerShell correct te kunnen interpreteren de syntaxis van de OData-filter gebruikt in AAD grafiek REST-aanroepen, moet u de backtick (aka: ernstig accent) 'escape' van het teken $-teken.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-123">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="bf1ff-124">Het teken backtick fungeert als [PowerShell van escape-teken](https://technet.microsoft.com/library/hh847755.aspx), zodat PowerShell een letterlijke interpretatie van het teken $ en te voorkomen dat deze als de naam van een PowerShell-variabele verwarrend (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-124">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="bf1ff-125">De focus van dit onderwerp is op de grafiek Explorer.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-125">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="bf1ff-126">Zie voor een voorbeeld van PowerShell [PowerShell-script](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="bf1ff-127">API-eindpunt</span><span class="sxs-lookup"><span data-stu-id="bf1ff-127">API Endpoint</span></span>
<span data-ttu-id="bf1ff-128">U kunt toegang tot deze API met behulp van de volgende URI:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-128">You can access this API using the following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="bf1ff-129">Er is geen limiet voor het aantal records dat wordt geretourneerd door de Azure AD-audit-API (OData paginering met).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-129">There is no limit on the number of records returned by the Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="bf1ff-130">Bekijk voor ondergrenzen voor de bewaarperiode op rapportagegegevens [bewaarbeleidsregels Reporting](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="bf1ff-131">Deze aanroep retourneert de gegevens in batches.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-131">This call returns the data in batches.</span></span> <span data-ttu-id="bf1ff-132">Elke batch heeft maximaal 1000 records.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="bf1ff-133">Als u de volgende batch met records, gebruikt u de volgende koppeling.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-133">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="bf1ff-134">De informatie skiptoken ophalen uit de eerste reeks geretourneerde records.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-134">Get the skiptoken information from the first set of returned records.</span></span> <span data-ttu-id="bf1ff-135">Het skip-token wordt aan het einde van het resultaat ingesteld.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-135">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="bf1ff-136">Ondersteunde filters</span><span class="sxs-lookup"><span data-stu-id="bf1ff-136">Supported filters</span></span>
<span data-ttu-id="bf1ff-137">U kunt beperken het aantal records dat wordt geretourneerd door een API-aanroep in de vorm van een filter.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-137">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="bf1ff-138">Voor aanmelden API van de bijbehorende gegevens, de volgende filters worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-138">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="bf1ff-139">**$top =\<aantal records moeten worden geretourneerd\>**  : het aantal geretourneerde records te beperken.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-139">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="bf1ff-140">Dit is een dure bewerking.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-140">This is an expensive operation.</span></span> <span data-ttu-id="bf1ff-141">U moet dit filter niet gebruiken als u wilt retourneren duizenden objecten.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-141">You should not use this filter if you want to return thousands of objects.</span></span>     
* <span data-ttu-id="bf1ff-142">**$filter =\<uw filterinstructie\>**  - om op te geven op basis van de ondersteunde filtervelden, het type van records die u belangrijk vindt</span><span class="sxs-lookup"><span data-stu-id="bf1ff-142">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="bf1ff-143">Ondersteunde filtervelden en -operators</span><span class="sxs-lookup"><span data-stu-id="bf1ff-143">Supported filter fields and operators</span></span>
<span data-ttu-id="bf1ff-144">Als u wilt opgeven welk type records die u belangrijk vindt, kunt u een filter-instructie die kan een bestand of een combinatie van de volgende filtervelden bevatten:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-144">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="bf1ff-145">[ActiviteitDatum](#activitydate) -definieert een datum of datumbereik</span><span class="sxs-lookup"><span data-stu-id="bf1ff-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="bf1ff-146">[categorie](#category) -definieert de categorie die u filteren wilt op.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-146">[category](#category) - defines the category you want to filter on.</span></span>
* <span data-ttu-id="bf1ff-147">[activityStatus](#activitystatus) -bepaalt de status van een activiteit</span><span class="sxs-lookup"><span data-stu-id="bf1ff-147">[activityStatus](#activitystatus) - defines the status of an activity</span></span>
* <span data-ttu-id="bf1ff-148">[activityType](#activitytype) -definieert het type van een activiteit</span><span class="sxs-lookup"><span data-stu-id="bf1ff-148">[activityType](#activitytype)  - defines the type of an activity</span></span>
* <span data-ttu-id="bf1ff-149">[activiteit](#activity) -definieert u de activiteit als tekenreeks</span><span class="sxs-lookup"><span data-stu-id="bf1ff-149">[activity](#activity) - defines the activity as string</span></span>  
* <span data-ttu-id="bf1ff-150">[naam van deacteur/](#actorname) -definieert de actor in de vorm van de naam van de actor</span><span class="sxs-lookup"><span data-stu-id="bf1ff-150">[actor/name](#actorname) -   defines the actor in form of the actor's name</span></span>
* <span data-ttu-id="bf1ff-151">[acteur/objectid](#actorobjectid) -definieert de actor in de vorm van de actor-ID</span><span class="sxs-lookup"><span data-stu-id="bf1ff-151">[actor/objectid](#actorobjectid) - defines the actor in form of the actor's ID</span></span>   
* <span data-ttu-id="bf1ff-152">[acteur/upn](#actorupn) -definieert de actor in de vorm van de actor principe (user Principal name)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-152">[actor/upn](#actorupn)  - defines the actor in form of the actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="bf1ff-153">[doelnaam/](#targetname) -definieert het doel in de vorm van de naam van de actor</span><span class="sxs-lookup"><span data-stu-id="bf1ff-153">[target/name](#targetname)  - defines the target in form of the actor's name</span></span>
* <span data-ttu-id="bf1ff-154">[doel/objectid](#targetobjectid) -definieert het doel in de vorm van de doel-ID</span><span class="sxs-lookup"><span data-stu-id="bf1ff-154">[target/objectid](#targetobjectid) - defines the target in form of the target's ID</span></span>  
* <span data-ttu-id="bf1ff-155">[doel/upn](#targetupn) -definieert de actor in de vorm van de actor principe (user Principal name)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-155">[target/upn](#targetupn) - defines the actor in form of the actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="bf1ff-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="bf1ff-156">activityDate</span></span>
<span data-ttu-id="bf1ff-157">**Operators ondersteund**: eq, ge RP, gt, lt</span><span class="sxs-lookup"><span data-stu-id="bf1ff-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="bf1ff-158">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="bf1ff-159">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-159">**Notes**:</span></span>

<span data-ttu-id="bf1ff-160">DateTime-waarde moet in UTC-notatie</span><span class="sxs-lookup"><span data-stu-id="bf1ff-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="bf1ff-161">category</span><span class="sxs-lookup"><span data-stu-id="bf1ff-161">category</span></span>

<span data-ttu-id="bf1ff-162">**Ondersteunde waarden**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-162">**Supported values**:</span></span>

| <span data-ttu-id="bf1ff-163">Category</span><span class="sxs-lookup"><span data-stu-id="bf1ff-163">Category</span></span>                         | <span data-ttu-id="bf1ff-164">Waarde</span><span class="sxs-lookup"><span data-stu-id="bf1ff-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="bf1ff-165">Hoofddirectory</span><span class="sxs-lookup"><span data-stu-id="bf1ff-165">Core Directory</span></span>                   | <span data-ttu-id="bf1ff-166">Directory</span><span class="sxs-lookup"><span data-stu-id="bf1ff-166">Directory</span></span> |
| <span data-ttu-id="bf1ff-167">Self-service voor wachtwoordbeheer</span><span class="sxs-lookup"><span data-stu-id="bf1ff-167">Self-service Password Management</span></span> | <span data-ttu-id="bf1ff-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="bf1ff-168">SSPR</span></span>      |
| <span data-ttu-id="bf1ff-169">Self-service voor groepsbeheer</span><span class="sxs-lookup"><span data-stu-id="bf1ff-169">Self-service Group Management</span></span>    | <span data-ttu-id="bf1ff-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="bf1ff-170">SSGM</span></span>      |
| <span data-ttu-id="bf1ff-171">Account inrichten</span><span class="sxs-lookup"><span data-stu-id="bf1ff-171">Account Provisioning</span></span>             | <span data-ttu-id="bf1ff-172">Sync</span><span class="sxs-lookup"><span data-stu-id="bf1ff-172">Sync</span></span>      |
| <span data-ttu-id="bf1ff-173">Automatische wachtwoordoverschakeling</span><span class="sxs-lookup"><span data-stu-id="bf1ff-173">Automated Password Rollover</span></span>      | <span data-ttu-id="bf1ff-174">Automatische wachtwoordoverschakeling</span><span class="sxs-lookup"><span data-stu-id="bf1ff-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="bf1ff-175">Identiteitsbeveiliging</span><span class="sxs-lookup"><span data-stu-id="bf1ff-175">Identity Protection</span></span>              | <span data-ttu-id="bf1ff-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="bf1ff-176">IdentityProtection</span></span> |
| <span data-ttu-id="bf1ff-177">Uitgenodigde gebruikers</span><span class="sxs-lookup"><span data-stu-id="bf1ff-177">Invited Users</span></span>                    | <span data-ttu-id="bf1ff-178">Uitgenodigde gebruikers</span><span class="sxs-lookup"><span data-stu-id="bf1ff-178">Invited Users</span></span> |
| <span data-ttu-id="bf1ff-179">MIM-service</span><span class="sxs-lookup"><span data-stu-id="bf1ff-179">MIM Service</span></span>                      | <span data-ttu-id="bf1ff-180">MIM-service</span><span class="sxs-lookup"><span data-stu-id="bf1ff-180">MIM Service</span></span> |



<span data-ttu-id="bf1ff-181">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="bf1ff-181">**Supported operators**: eq</span></span>

<span data-ttu-id="bf1ff-182">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="bf1ff-183">ActivityStatus</span><span class="sxs-lookup"><span data-stu-id="bf1ff-183">activityStatus</span></span>

<span data-ttu-id="bf1ff-184">**Ondersteunde waarden**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-184">**Supported values**:</span></span>

| <span data-ttu-id="bf1ff-185">Activiteitsstatus</span><span class="sxs-lookup"><span data-stu-id="bf1ff-185">Activity Status</span></span> | <span data-ttu-id="bf1ff-186">Waarde</span><span class="sxs-lookup"><span data-stu-id="bf1ff-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="bf1ff-187">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="bf1ff-187">Success</span></span>         | <span data-ttu-id="bf1ff-188">0</span><span class="sxs-lookup"><span data-stu-id="bf1ff-188">0</span></span>     |
| <span data-ttu-id="bf1ff-189">Fout</span><span class="sxs-lookup"><span data-stu-id="bf1ff-189">Failure</span></span>         | <span data-ttu-id="bf1ff-190">- 1</span><span class="sxs-lookup"><span data-stu-id="bf1ff-190">- 1</span></span>   |

<span data-ttu-id="bf1ff-191">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="bf1ff-191">**Supported operators**: eq</span></span>

<span data-ttu-id="bf1ff-192">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="bf1ff-193">activityType</span><span class="sxs-lookup"><span data-stu-id="bf1ff-193">activityType</span></span>
<span data-ttu-id="bf1ff-194">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="bf1ff-194">**Supported operators**: eq</span></span>

<span data-ttu-id="bf1ff-195">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="bf1ff-196">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-196">**Notes**:</span></span>

<span data-ttu-id="bf1ff-197">hoofdlettergevoelig</span><span class="sxs-lookup"><span data-stu-id="bf1ff-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="bf1ff-198">Activiteit</span><span class="sxs-lookup"><span data-stu-id="bf1ff-198">activity</span></span>
<span data-ttu-id="bf1ff-199">**Operators ondersteund**: eq, bevat, startsWith</span><span class="sxs-lookup"><span data-stu-id="bf1ff-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="bf1ff-200">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="bf1ff-201">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-201">**Notes**:</span></span>

<span data-ttu-id="bf1ff-202">hoofdlettergevoelig</span><span class="sxs-lookup"><span data-stu-id="bf1ff-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="bf1ff-203">naam van de acteur /</span><span class="sxs-lookup"><span data-stu-id="bf1ff-203">actor/name</span></span>
<span data-ttu-id="bf1ff-204">**Operators ondersteund**: eq, bevat, startsWith</span><span class="sxs-lookup"><span data-stu-id="bf1ff-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="bf1ff-205">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="bf1ff-206">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-206">**Notes**:</span></span>

<span data-ttu-id="bf1ff-207">Niet-hoofdlettergevoelige</span><span class="sxs-lookup"><span data-stu-id="bf1ff-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="bf1ff-208">acteur/objectId</span><span class="sxs-lookup"><span data-stu-id="bf1ff-208">actor/objectId</span></span>
<span data-ttu-id="bf1ff-209">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="bf1ff-209">**Supported operators**: eq</span></span>

<span data-ttu-id="bf1ff-210">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="bf1ff-211">doelnaam /</span><span class="sxs-lookup"><span data-stu-id="bf1ff-211">target/name</span></span>
<span data-ttu-id="bf1ff-212">**Operators ondersteund**: eq, bevat, startsWith</span><span class="sxs-lookup"><span data-stu-id="bf1ff-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="bf1ff-213">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="bf1ff-214">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-214">**Notes**:</span></span>

<span data-ttu-id="bf1ff-215">Niet-hoofdlettergevoelige</span><span class="sxs-lookup"><span data-stu-id="bf1ff-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="bf1ff-216">doel/upn</span><span class="sxs-lookup"><span data-stu-id="bf1ff-216">target/upn</span></span>
<span data-ttu-id="bf1ff-217">**Operators ondersteund**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="bf1ff-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="bf1ff-218">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="bf1ff-219">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-219">**Notes**:</span></span>

* <span data-ttu-id="bf1ff-220">Niet-hoofdlettergevoelige</span><span class="sxs-lookup"><span data-stu-id="bf1ff-220">Case-insensitive</span></span>
* <span data-ttu-id="bf1ff-221">U moet de volledige naamruimte toevoegen bij het opvragen van Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="bf1ff-221">You need to add the full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="bf1ff-222">doel/objectId</span><span class="sxs-lookup"><span data-stu-id="bf1ff-222">target/objectId</span></span>
<span data-ttu-id="bf1ff-223">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="bf1ff-223">**Supported operators**: eq</span></span>

<span data-ttu-id="bf1ff-224">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="bf1ff-225">acteur/upn</span><span class="sxs-lookup"><span data-stu-id="bf1ff-225">actor/upn</span></span>
<span data-ttu-id="bf1ff-226">**Operators ondersteund**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="bf1ff-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="bf1ff-227">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="bf1ff-228">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-228">**Notes**:</span></span>

* <span data-ttu-id="bf1ff-229">Niet-hoofdlettergevoelige</span><span class="sxs-lookup"><span data-stu-id="bf1ff-229">Case-insensitive</span></span> 
* <span data-ttu-id="bf1ff-230">U moet de volledige naamruimte toevoegen bij het opvragen van Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="bf1ff-230">You need to add the full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="bf1ff-231">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bf1ff-231">Next Steps</span></span>
* <span data-ttu-id="bf1ff-232">Wilt u ziet u voorbeelden van gefilterde systeemactiviteiten?</span><span class="sxs-lookup"><span data-stu-id="bf1ff-232">Do you want to see examples for filtered system activities?</span></span> <span data-ttu-id="bf1ff-233">Bekijk de [voorbeelden van Azure Active Directory-audit API](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-233">Check out the [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="bf1ff-234">Wilt u meer informatie over de Azure AD rapportage-API?</span><span class="sxs-lookup"><span data-stu-id="bf1ff-234">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="bf1ff-235">Zie [aan de slag met Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-235">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>


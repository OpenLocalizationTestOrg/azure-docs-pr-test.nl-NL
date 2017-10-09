---
title: activiteitenrapport aaaAzure Active Directory-aanmeldingspagina API-referentiemateriaal | Microsoft Docs
description: Naslaginformatie voor hello Azure Active Directory-aanmeldingspagina activiteitenrapport API
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="2fa94-103">Azure Active Directory aanmeldingsactiviteiten rapport API-referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="2fa94-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="2fa94-104">In dit onderwerp maakt deel uit van een verzameling van onderwerpen over hello Azure Active Directory rapportage-API.</span><span class="sxs-lookup"><span data-stu-id="2fa94-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="2fa94-105">Rapportage van Azure AD biedt u een API waarmee u kunt rapportgegevens voor tooaccess aanmeldingsactiviteiten met code of gerelateerde hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="2fa94-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="2fa94-106">Hallo-bereik van dit onderwerp is tooprovide u met naslaginformatie over Hallo **aanmelden activiteit rapport API**.</span><span class="sxs-lookup"><span data-stu-id="2fa94-106">hello scope of this topic is tooprovide you with reference information about hello **sign-in activity report API**.</span></span>

<span data-ttu-id="2fa94-107">Zie:</span><span class="sxs-lookup"><span data-stu-id="2fa94-107">See:</span></span>

* <span data-ttu-id="2fa94-108">[Aanmelden activiteiten](active-directory-reporting-azure-portal.md#activity-reports) voor meer conceptuele informatie</span><span class="sxs-lookup"><span data-stu-id="2fa94-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="2fa94-109">[Aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md) voor meer informatie over Hallo rapportage-API.</span><span class="sxs-lookup"><span data-stu-id="2fa94-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="who-can-access-hello-api-data"></a><span data-ttu-id="2fa94-110">Wie toegang heeft tot Hallo API gegevens?</span><span class="sxs-lookup"><span data-stu-id="2fa94-110">Who can access hello API data?</span></span>
* <span data-ttu-id="2fa94-111">Gebruikers- en Service-Principals Hallo beheerder beveiliging of beveiliging lezer rol</span><span class="sxs-lookup"><span data-stu-id="2fa94-111">Users and Service Principals in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="2fa94-112">Globale beheerders</span><span class="sxs-lookup"><span data-stu-id="2fa94-112">Global Admins</span></span>
* <span data-ttu-id="2fa94-113">Elke app die autorisatie tooaccess Hallo API is (app autorisatie worden instellingen slechts op basis van toestemming van de globale beheerder)</span><span class="sxs-lookup"><span data-stu-id="2fa94-113">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="2fa94-114">tooconfigure toegang voor een tooaccess Toepassingsbeveiliging API's zoals signin-gebeurtenissen, gebruik Hallo PowerShell tooadd Hallo toepassingen Service-Principal te volgen in de rol van de lezer van de beveiliging Hallo</span><span class="sxs-lookup"><span data-stu-id="2fa94-114">tooconfigure access for an application tooaccess security APIs such as signin events, use hello following PowerShell tooadd hello applications Service Principal into hello Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="2fa94-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2fa94-115">Prerequisites</span></span>
<span data-ttu-id="2fa94-116">in deze lijst via tooaccess Hallo reporting API, moet u hebben:</span><span class="sxs-lookup"><span data-stu-id="2fa94-116">tooaccess this report through hello reporting API, you must have:</span></span>

* <span data-ttu-id="2fa94-117">Een [Azure Active Directory Premium P1 of P2 edition](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="2fa94-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="2fa94-118">Voltooide Hallo [vereisten tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="2fa94-118">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="2fa94-119">Toegang tot Hallo-API</span><span class="sxs-lookup"><span data-stu-id="2fa94-119">Accessing hello API</span></span>
<span data-ttu-id="2fa94-120">U kunt deze API voor installatie zonder toezicht benaderen via Hallo [grafiek Explorer](https://graphexplorer2.cloudapp.net) of programmatisch met bijvoorbeeld PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2fa94-120">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="2fa94-121">In de volgorde voor PowerShell toocorrectly interpreteren Hallo OData-filtersyntaxis gebruikt in AAD grafiek REST-aanroepen, moet u Hallo backtick (aka: ernstig accent) teken te 'escape' hello $-teken.</span><span class="sxs-lookup"><span data-stu-id="2fa94-121">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="2fa94-122">Hallo backtick teken fungeert als [PowerShell van escape-teken](https://technet.microsoft.com/library/hh847755.aspx)PowerShell toodo zodat een letterlijke interpretatie van Hallo $-teken en te voorkomen dat deze als de naam van een PowerShell-variabele verwarrend (ie: $filter).</span><span class="sxs-lookup"><span data-stu-id="2fa94-122">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="2fa94-123">in dit onderwerp Hallo richt zich op Hallo grafiek Explorer.</span><span class="sxs-lookup"><span data-stu-id="2fa94-123">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="2fa94-124">Zie voor een voorbeeld van PowerShell [PowerShell-script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="2fa94-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="2fa94-125">API-eindpunt</span><span class="sxs-lookup"><span data-stu-id="2fa94-125">API Endpoint</span></span>
<span data-ttu-id="2fa94-126">U kunt toegang tot deze API met behulp van Hallo basis-URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="2fa94-126">You can access this API using hello following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="2fa94-127">Vanwege toohello hoeveelheid gegevens die heeft deze API een limiet van 1 miljoen records geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="2fa94-127">Due toohello volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="2fa94-128">Deze aanroep retourneert Hallo gegevens in batches.</span><span class="sxs-lookup"><span data-stu-id="2fa94-128">This call returns hello data in batches.</span></span> <span data-ttu-id="2fa94-129">Elke batch heeft maximaal 1000 records.</span><span class="sxs-lookup"><span data-stu-id="2fa94-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="2fa94-130">tooget hello volgende batch van records, volgende Hallo-verbinding gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2fa94-130">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="2fa94-131">Hallo ophalen [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) informatie uit de eerste set Hallo van de geretourneerde records.</span><span class="sxs-lookup"><span data-stu-id="2fa94-131">Get hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from hello first set of returned records.</span></span> <span data-ttu-id="2fa94-132">Hallo skip-token worden achter Hallo Hallo resultatenset.</span><span class="sxs-lookup"><span data-stu-id="2fa94-132">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="2fa94-133">Ondersteunde filters</span><span class="sxs-lookup"><span data-stu-id="2fa94-133">Supported filters</span></span>
<span data-ttu-id="2fa94-134">U kunt kleiner Hallo aantal records dat wordt geretourneerd door een API-aanroep in de vorm van een filter.</span><span class="sxs-lookup"><span data-stu-id="2fa94-134">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="2fa94-135">Voor aanmelden API worden gerelateerde gegevens, Hallo na filters ondersteund:</span><span class="sxs-lookup"><span data-stu-id="2fa94-135">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="2fa94-136">**$top =\<aantal records toobe geretourneerd\>**  -toolimit Hallo aantal geretourneerde records.</span><span class="sxs-lookup"><span data-stu-id="2fa94-136">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="2fa94-137">Dit is een dure bewerking.</span><span class="sxs-lookup"><span data-stu-id="2fa94-137">This is an expensive operation.</span></span> <span data-ttu-id="2fa94-138">U moet dit filter niet gebruiken als u wilt dat tooreturn duizenden objecten.</span><span class="sxs-lookup"><span data-stu-id="2fa94-138">You should not use this filter if you want tooreturn thousands of objects.</span></span>  
* <span data-ttu-id="2fa94-139">**$filter =\<uw filterinstructie\>**  -toospecify op basis van ondersteunde filtervelden, registreert u het belangrijkst Hallo type Hallo</span><span class="sxs-lookup"><span data-stu-id="2fa94-139">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="2fa94-140">Ondersteunde filtervelden en -operators</span><span class="sxs-lookup"><span data-stu-id="2fa94-140">Supported filter fields and operators</span></span>
<span data-ttu-id="2fa94-141">toospecify hello type records die u belangrijk vindt, kunt u een filter-instructie die kan een bestand of een combinatie van Hallo na filtervelden bevatten:</span><span class="sxs-lookup"><span data-stu-id="2fa94-141">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="2fa94-142">[signinDateTime](#signindatetime) -definieert een datum of datumbereik</span><span class="sxs-lookup"><span data-stu-id="2fa94-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="2fa94-143">[userId](#userid) -definieert een specifieke gebruiker op basis van Hallo-gebruikers-ID.</span><span class="sxs-lookup"><span data-stu-id="2fa94-143">[userId](#userid) - defines a specific user based hello user's ID.</span></span>
* <span data-ttu-id="2fa94-144">[userPrincipalName](#userprincipalname) -definieert van een specifieke gebruiker op basis van Hallo gebruiker UPN (User Principal Name)</span><span class="sxs-lookup"><span data-stu-id="2fa94-144">[userPrincipalName](#userprincipalname) - defines a specific user based hello user's user principal name (UPN)</span></span>
* <span data-ttu-id="2fa94-145">[appId](#appid) -ID van een specifieke app op basis van Hallo app definieert</span><span class="sxs-lookup"><span data-stu-id="2fa94-145">[appId](#appid) - defines a specific app based hello app's ID</span></span>
* <span data-ttu-id="2fa94-146">[appDisplayName](#appdisplayname) -definieert weergavenaam voor een specifieke app op basis van Hallo-app</span><span class="sxs-lookup"><span data-stu-id="2fa94-146">[appDisplayName](#appdisplayname) - defines a specific app based hello app's display name</span></span>
* <span data-ttu-id="2fa94-147">[loginStatus](#loginStatus) -definieert Hallo status van Hallo aanmeldingen (geslaagd / fout)</span><span class="sxs-lookup"><span data-stu-id="2fa94-147">[loginStatus](#loginStatus) - defines hello status of hello logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="2fa94-148">Wanneer u grafiek Explorer gebruikt, moet u Hallo toouse Hallo juist geldt voor elke letter filter-velden.</span><span class="sxs-lookup"><span data-stu-id="2fa94-148">When using Graph Explorer, you hello need toouse hello correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="2fa94-149">toonarrow u Hallo bereik van Hallo gegevens geretourneerd, kunt u combinaties van Hallo ondersteund filters en filtervelden maken.</span><span class="sxs-lookup"><span data-stu-id="2fa94-149">toonarrow down hello scope of hello returned data, you can build combinations of hello supported filters and filter fields.</span></span> <span data-ttu-id="2fa94-150">Bijvoorbeeld: hello volgende instructie retourneert Hallo bovenste 10 records tussen 1 juli 2016 en juli 6 2016:</span><span class="sxs-lookup"><span data-stu-id="2fa94-150">For example, hello following statement returns hello top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="2fa94-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="2fa94-151">signinDateTime</span></span>
<span data-ttu-id="2fa94-152">**Operators ondersteund**: eq, ge RP, gt, lt</span><span class="sxs-lookup"><span data-stu-id="2fa94-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="2fa94-153">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-153">**Example**:</span></span>

<span data-ttu-id="2fa94-154">Met behulp van een specifieke datum</span><span class="sxs-lookup"><span data-stu-id="2fa94-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="2fa94-155">Met behulp van een datumbereik</span><span class="sxs-lookup"><span data-stu-id="2fa94-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="2fa94-156">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-156">**Notes**:</span></span>

<span data-ttu-id="2fa94-157">Hallo datetime-parameter moet zich bevinden in Hallo UTC-notatie</span><span class="sxs-lookup"><span data-stu-id="2fa94-157">hello datetime parameter should be in hello UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="2fa94-158">Gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="2fa94-158">userId</span></span>
<span data-ttu-id="2fa94-159">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="2fa94-159">**Supported operators**: eq</span></span>

<span data-ttu-id="2fa94-160">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="2fa94-161">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-161">**Notes**:</span></span>

<span data-ttu-id="2fa94-162">Hallo-waarde van de gebruikers-id is een string-waarde</span><span class="sxs-lookup"><span data-stu-id="2fa94-162">hello value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="2fa94-163">UserPrincipalName</span><span class="sxs-lookup"><span data-stu-id="2fa94-163">userPrincipalName</span></span>
<span data-ttu-id="2fa94-164">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="2fa94-164">**Supported operators**: eq</span></span>

<span data-ttu-id="2fa94-165">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="2fa94-166">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-166">**Notes**:</span></span>

<span data-ttu-id="2fa94-167">Hallo-waarde van userPrincipalName is de waarde van een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="2fa94-167">hello value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="2fa94-168">AppId</span><span class="sxs-lookup"><span data-stu-id="2fa94-168">appId</span></span>
<span data-ttu-id="2fa94-169">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="2fa94-169">**Supported operators**: eq</span></span>

<span data-ttu-id="2fa94-170">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="2fa94-171">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-171">**Notes**:</span></span>

<span data-ttu-id="2fa94-172">Hallo-waarde van de appId is een string-waarde</span><span class="sxs-lookup"><span data-stu-id="2fa94-172">hello value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="2fa94-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="2fa94-173">appDisplayName</span></span>
<span data-ttu-id="2fa94-174">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="2fa94-174">**Supported operators**: eq</span></span>

<span data-ttu-id="2fa94-175">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="2fa94-176">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-176">**Notes**:</span></span>

<span data-ttu-id="2fa94-177">Hallo-waarde van appDisplayName is een string-waarde</span><span class="sxs-lookup"><span data-stu-id="2fa94-177">hello value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="2fa94-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="2fa94-178">loginStatus</span></span>
<span data-ttu-id="2fa94-179">**Operators ondersteund**: eq</span><span class="sxs-lookup"><span data-stu-id="2fa94-179">**Supported operators**: eq</span></span>

<span data-ttu-id="2fa94-180">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="2fa94-181">**Opmerkingen bij de**:</span><span class="sxs-lookup"><span data-stu-id="2fa94-181">**Notes**:</span></span>

<span data-ttu-id="2fa94-182">Er zijn twee opties voor Hallo loginStatus: 0 - geslaagd, 1 - fout</span><span class="sxs-lookup"><span data-stu-id="2fa94-182">There are two options for hello loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="2fa94-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2fa94-183">Next steps</span></span>
* <span data-ttu-id="2fa94-184">Wilt u toosee voorbeelden voor gefilterde activiteiten aanmelden?</span><span class="sxs-lookup"><span data-stu-id="2fa94-184">Do you want toosee examples for filtered sign-in activities?</span></span> <span data-ttu-id="2fa94-185">Bekijk Hallo [Azure Active Directory aanmeldingsactiviteiten rapport API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2fa94-185">Check out hello [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="2fa94-186">Wilt u meer informatie over reporting hello Azure AD-API tooknow?</span><span class="sxs-lookup"><span data-stu-id="2fa94-186">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="2fa94-187">Zie [aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="2fa94-187">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>


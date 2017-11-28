---
title: 'Azure Active Directory B2C: Gebruik reporting API samples en definities | Microsoft Docs'
description: Handleiding en voorbeelden op rapporten op Azure AD B2C-tenant ophalen van gebruikers, verificaties en multi-factor Authentication-oproepen
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a><span data-ttu-id="793b6-103">Toegang tot gebruiksrapporten in Azure AD B2C via Hallo rapportage-API</span><span class="sxs-lookup"><span data-stu-id="793b6-103">Accessing usage reports in Azure AD B2C via hello reporting API</span></span>

<span data-ttu-id="793b6-104">Azure Active Directory B2C (Azure AD B2C) biedt verificatie op basis van de gebruiker zich aanmelden en Azure multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="793b6-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="793b6-105">Verificatie is bestemd voor eindgebruikers van uw toepassing familie over id-providers.</span><span class="sxs-lookup"><span data-stu-id="793b6-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="793b6-106">Als u weet dat het aantal gebruikers die zijn geregistreerd in Hallo-tenant, ze gebruikt tooregister en het aantal authenticaties Hallo Hallo-providers per type Hallo kunt u beantwoorden van vragen als:</span><span class="sxs-lookup"><span data-stu-id="793b6-106">When you know hello number of users registered in hello tenant, hello providers they used tooregister, and hello number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="793b6-107">Hoeveel gebruikers vanuit elk type id-provider (bijvoorbeeld een account van Microsoft of LinkedIn) hebt geregistreerd in het Hallo laatste 10 dagen?</span><span class="sxs-lookup"><span data-stu-id="793b6-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in hello last 10 days?</span></span>
* <span data-ttu-id="793b6-108">Het aantal authenticaties met multi-factor Authentication zijn in de afgelopen maand Hallo met succes voltooid?</span><span class="sxs-lookup"><span data-stu-id="793b6-108">How many authentications using Multi-Factor Authentication have completed successfully in hello last month?</span></span>
* <span data-ttu-id="793b6-109">Hoeveel aanmelding in gebaseerd verificaties zijn deze maand voltooid?</span><span class="sxs-lookup"><span data-stu-id="793b6-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="793b6-110">Per dag?</span><span class="sxs-lookup"><span data-stu-id="793b6-110">Per day?</span></span> <span data-ttu-id="793b6-111">Per toepassing?</span><span class="sxs-lookup"><span data-stu-id="793b6-111">Per application?</span></span>
* <span data-ttu-id="793b6-112">Hoe kan ik schatten Hallo verwachte maandelijkse kosten van de activiteit van mijn Azure AD B2C-tenant?</span><span class="sxs-lookup"><span data-stu-id="793b6-112">How can I estimate hello expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="793b6-113">Dit artikel is gericht op de activiteit toobilling rapporten die zijn gekoppeld, die is gebaseerd op Hallo aantal gebruikers, factureerbare aanmelding in gebaseerd verificaties en multi-factor Authentication-oproepen.</span><span class="sxs-lookup"><span data-stu-id="793b6-113">This article focuses on reports tied toobilling activity, which is based on hello number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="793b6-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="793b6-114">Prerequisites</span></span>
<span data-ttu-id="793b6-115">Voordat u begint, moet u toocomplete Hallo stappen in [vereisten tooaccess hello Azure AD-rapportage API's](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="793b6-115">Before you get started, you need toocomplete hello steps in [Prerequisites tooaccess hello Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="793b6-116">Maken van een toepassing, een geheim voor het verkrijgen en verleen deze toegang hebben tot rechten tooyour Azure AD B2C-tenant-rapporten.</span><span class="sxs-lookup"><span data-stu-id="793b6-116">Create an application, obtain a secret for it, and grant it access rights tooyour Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="793b6-117">*Script Bash* en *pythonscript* voorbeelden vindt u ook hier.</span><span class="sxs-lookup"><span data-stu-id="793b6-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="793b6-118">PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="793b6-118">PowerShell script</span></span>
<span data-ttu-id="793b6-119">Dit script wordt getoond hoe u Hallo vier gebruiksrapporten via Hallo `TimeStamp` parameter en Hallo `ApplicationId` filter.</span><span class="sxs-lookup"><span data-stu-id="793b6-119">This script demonstrates hello creation of four usage reports by using hello `TimeStamp` parameter and hello `ApplicationId` filter.</span></span>

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="793b6-120">Gebruik rapportdefinities</span><span class="sxs-lookup"><span data-stu-id="793b6-120">Usage report definitions</span></span>
* <span data-ttu-id="793b6-121">**tenantUserCount**: aantal gebruikers in de tenant door type id-provider per dag in Hallo HALLO hallo afgelopen 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="793b6-121">**tenantUserCount**: hello number of users in hello tenant by type of identity provider, per day in hello last 30 days.</span></span> <span data-ttu-id="793b6-122">(U kunt desgewenst een `TimeStamp` -filter biedt gebruiker tellingen van een opgegeven datum toohello huidige datum).</span><span class="sxs-lookup"><span data-stu-id="793b6-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date toohello current date).</span></span> <span data-ttu-id="793b6-123">Hallo rapport biedt:</span><span class="sxs-lookup"><span data-stu-id="793b6-123">hello report provides:</span></span>
  * <span data-ttu-id="793b6-124">**TotalUserCount**: nummer van alle gebruikersobjecten Hallo.</span><span class="sxs-lookup"><span data-stu-id="793b6-124">**TotalUserCount**: hello number of all user objects.</span></span>
  * <span data-ttu-id="793b6-125">**OtherUserCount**: Hallo aantal Azure Active Directory-gebruikers (geen Azure AD B2C-gebruikers).</span><span class="sxs-lookup"><span data-stu-id="793b6-125">**OtherUserCount**: hello number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="793b6-126">**LocalUserCount**: Hallo aantal Azure AD B2C-gebruikersaccounts met referenties lokale toohello Azure AD B2C-tenant is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="793b6-126">**LocalUserCount**: hello number of Azure AD B2C user accounts created with credentials local toohello Azure AD B2C tenant.</span></span>

* <span data-ttu-id="793b6-127">**AlternateIdUserCount**: aantal gebruikers van Azure AD B2C Hallo geregistreerd bij de externe id-providers (bijvoorbeeld, Facebook, een Microsoft-account of een andere Azure Active Directory-tenant, ook wel aangeduid tooas een `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="793b6-127">**AlternateIdUserCount**: hello number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred tooas an `OrgId`).</span></span>

* <span data-ttu-id="793b6-128">**b2cAuthenticationCountSummary**: samenvatting van Hallo dagelijks aantal factureerbare verificaties via Hallo afgelopen 30 dagen door de dag en het type verificatiestroom.</span><span class="sxs-lookup"><span data-stu-id="793b6-128">**b2cAuthenticationCountSummary**: Summary of hello daily number of billable authentications over hello last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="793b6-129">**b2cAuthenticationCount**: aantal verificaties Hallo binnen een periode.</span><span class="sxs-lookup"><span data-stu-id="793b6-129">**b2cAuthenticationCount**: hello number of authentications within a time period.</span></span> <span data-ttu-id="793b6-130">Hallo standaardwaarde is Hallo afgelopen 30 dagen.</span><span class="sxs-lookup"><span data-stu-id="793b6-130">hello default is hello last 30 days.</span></span>  <span data-ttu-id="793b6-131">(Optioneel: Hallo begin en eind `TimeStamp` parameters definiëren een specifiek tijdstip periode.) Hallo uitvoer bevat `StartTimeStamp` (vroegste datum van activiteiten voor deze tenant) en `EndTimeStamp` (laatste update).</span><span class="sxs-lookup"><span data-stu-id="793b6-131">(Optional: hello beginning and ending `TimeStamp` parameters define a specific time period.) hello output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="793b6-132">**b2cMfaRequestCountSummary**: samenvatting van Hallo dagelijks aantal multi-factor Authentication-oproepen per dag en het type (SMS of stem).</span><span class="sxs-lookup"><span data-stu-id="793b6-132">**b2cMfaRequestCountSummary**: Summary of hello daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="793b6-133">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="793b6-133">Limitations</span></span>
<span data-ttu-id="793b6-134">Aantal gebruikersgegevens wordt elke 24 uur voor too48 vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="793b6-134">User count data is refreshed every 24 too48 hours.</span></span> <span data-ttu-id="793b6-135">Authenticaties worden meerdere keren per dag bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="793b6-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="793b6-136">Wanneer u Hallo `ApplicationId` filter, een antwoord leeg rapport kan worden veroorzaakt door tooone van de volgende voorwaarden:</span><span class="sxs-lookup"><span data-stu-id="793b6-136">When using hello `ApplicationId` filter, an empty report response can be due tooone of following conditions:</span></span>
  * <span data-ttu-id="793b6-137">Hallo toepassings-ID bestaat niet in Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="793b6-137">hello application ID does not exist in hello tenant.</span></span> <span data-ttu-id="793b6-138">Zorg ervoor dat deze juist is.</span><span class="sxs-lookup"><span data-stu-id="793b6-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="793b6-139">Hallo toepassings-ID bestaat, maar er zijn geen gegevens gevonden in Hallo rapportageperiode.</span><span class="sxs-lookup"><span data-stu-id="793b6-139">hello application ID exists, but no data was found in hello reporting period.</span></span> <span data-ttu-id="793b6-140">Herzie de datum/tijd-parameters.</span><span class="sxs-lookup"><span data-stu-id="793b6-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="793b6-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="793b6-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="793b6-142">Maandelijkse factuur schattingen voor Azure AD</span><span class="sxs-lookup"><span data-stu-id="793b6-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="793b6-143">In combinatie met [Hallo meest recente prijzen beschikbaar Azure AD B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/), u kunt schatten dagelijkse, wekelijkse en maandelijkse Azure-verbruik.</span><span class="sxs-lookup"><span data-stu-id="793b6-143">When combined with [hello most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="793b6-144">Een schatting is vooral nuttig wanneer u van plan bent om wijzigingen in gedrag die voor de totale kosten gevolgen mogelijk van de tenant.</span><span class="sxs-lookup"><span data-stu-id="793b6-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="793b6-145">U kunt bekijken werkelijke kosten in uw [Azure-abonnement gekoppeld](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="793b6-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="793b6-146">Opties voor andere uitvoerindelingen</span><span class="sxs-lookup"><span data-stu-id="793b6-146">Options for other output formats</span></span>
<span data-ttu-id="793b6-147">Hallo ziet volgende code u voorbeelden van het verzenden van uitvoer tooJSON, een lijst met waarden van naam en XML:</span><span class="sxs-lookup"><span data-stu-id="793b6-147">hello following code shows examples of sending output tooJSON, a name value list, and XML:</span></span>
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```

---
title: aaaAzure Active Directory-aanmeldingspagina activiteit rapport API samples | Microsoft Docs
description: Hoe tooget gestart Hello Azure Active Directory rapportage-API
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: c41c1489-726b-4d3f-81d6-83beb932df9c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d4fbbea95fe0b52828673b997681ae37481e21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="e678b-103">Azure Active Directory aanmeldingsactiviteiten rapport API-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="e678b-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="e678b-104">In dit onderwerp maakt deel uit van een verzameling van onderwerpen over hello Azure Active Directory rapportage-API.</span><span class="sxs-lookup"><span data-stu-id="e678b-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="e678b-105">Rapportage van Azure AD biedt u een API waarmee u tooaccess aanmeldingsactiviteiten gegevens met code of bijbehorende hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="e678b-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="e678b-106">Hallo bereik van dit onderwerp is tooprovide u met voorbeeld de code voor Hallo **aanmelden activiteit API**.</span><span class="sxs-lookup"><span data-stu-id="e678b-106">hello scope of this topic is tooprovide you with sample code for hello **sign-in activity API**.</span></span>

<span data-ttu-id="e678b-107">Zie:</span><span class="sxs-lookup"><span data-stu-id="e678b-107">See:</span></span>

* <span data-ttu-id="e678b-108">[Controlelogboeken](active-directory-reporting-azure-portal.md#activity-reports) voor meer conceptuele informatie</span><span class="sxs-lookup"><span data-stu-id="e678b-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="e678b-109">[Aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md) voor meer informatie over Hallo rapportage-API.</span><span class="sxs-lookup"><span data-stu-id="e678b-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e678b-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e678b-110">Prerequisites</span></span>
<span data-ttu-id="e678b-111">Voordat u Hallo voorbeelden in dit onderwerp gebruiken kunt, moet u toocomplete hello [vereisten tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="e678b-111">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="e678b-112">PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="e678b-112">PowerShell script</span></span>
    # This script will require hello Web Application and permissions setup in Azure Active Directory
    $ClientID       = "<clientId>"             # Should be a ~35 character string insert your info here
    $ClientSecret   = "<clientSecret>"         # Should be a ~44 character string insert your info here
    $loginURL       = "https://login.microsoftonline.com/"
    $tenantdomain   = "<tenantDomain>"
    $ daterange            # For example, contoso.onmicrosoft.com

    $7daysago = "{0:s}" -f (get-date).AddDays(-7) + "Z"
    # or, AddMinutes(-5)

    Write-Output $7daysago

    # Get an Oauth 2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}

    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    if ($oauth.access_token -ne $null) {
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    $url = "https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&`$filter=signinDateTime ge $7daysago"

    $i=0

    Do{
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        Write-Output "Save hello output tooa file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-hello-script"></a><span data-ttu-id="e678b-113">Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e678b-113">Executing hello script</span></span>
<span data-ttu-id="e678b-114">Eenmaal u hebt bewerkt Hallo-script uitvoeren en controleren dat die Hallo verwachte gegevens van Hallo controlerapport logboeken worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="e678b-114">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="e678b-115">Hallo-script retourneert de uitvoer van Hallo aanmelden rapport in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="e678b-115">hello script returns output from hello sign-in report in JSON format.</span></span> <span data-ttu-id="e678b-116">Maakt ook een `SigninActivities.json` bestand Hello dezelfde uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e678b-116">It also creates an `SigninActivities.json` file with hello same output.</span></span> <span data-ttu-id="e678b-117">U kunt experimenteren door Hallo script tooreturn gegevens van andere rapporten en het commentaar Hallo-uitvoerindelingen die niet hoeven te passen.</span><span class="sxs-lookup"><span data-stu-id="e678b-117">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e678b-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e678b-118">Next Steps</span></span>
* <span data-ttu-id="e678b-119">Wilt u toocustomize Hallo voorbeelden in dit onderwerp?</span><span class="sxs-lookup"><span data-stu-id="e678b-119">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="e678b-120">Bekijk Hallo [Azure Active Directory aanmeldingsactiviteiten API-referentiemateriaal](active-directory-reporting-api-sign-in-activity-reference.md).</span><span class="sxs-lookup"><span data-stu-id="e678b-120">Check out hello [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="e678b-121">Als u wilt dat een volledig overzicht van het gebruik van toosee Hallo van Azure Active Directory rapportage-API, Zie [aan de slag met Azure Active Directory-rapportage API Hallo](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e678b-121">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="e678b-122">Als u toofind voor meer informatie over Azure Active Directory-rapportage wilt, Zie Hallo [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e678b-122">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  


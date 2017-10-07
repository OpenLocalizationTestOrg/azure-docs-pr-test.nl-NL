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
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a>Azure Active Directory aanmeldingsactiviteiten rapport API-voorbeelden
In dit onderwerp maakt deel uit van een verzameling van onderwerpen over hello Azure Active Directory rapportage-API.  
Rapportage van Azure AD biedt u een API waarmee u tooaccess aanmeldingsactiviteiten gegevens met code of bijbehorende hulpprogramma's.  
Hallo bereik van dit onderwerp is tooprovide u met voorbeeld de code voor Hallo **aanmelden activiteit API**.

Zie:

* [Controlelogboeken](active-directory-reporting-azure-portal.md#activity-reports) voor meer conceptuele informatie
* [Aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md) voor meer informatie over Hallo rapportage-API.


## <a name="prerequisites"></a>Vereisten
Voordat u Hallo voorbeelden in dit onderwerp gebruiken kunt, moet u toocomplete hello [vereisten tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).  

## <a name="powershell-script"></a>PowerShell-script
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




## <a name="executing-hello-script"></a>Hallo-script uitvoeren
Eenmaal u hebt bewerkt Hallo-script uitvoeren en controleren dat die Hallo verwachte gegevens van Hallo controlerapport logboeken worden geretourneerd.

Hallo-script retourneert de uitvoer van Hallo aanmelden rapport in JSON-indeling. Maakt ook een `SigninActivities.json` bestand Hello dezelfde uitvoer. U kunt experimenteren door Hallo script tooreturn gegevens van andere rapporten en het commentaar Hallo-uitvoerindelingen die niet hoeven te passen.

## <a name="next-steps"></a>Volgende stappen
* Wilt u toocustomize Hallo voorbeelden in dit onderwerp? Bekijk Hallo [Azure Active Directory aanmeldingsactiviteiten API-referentiemateriaal](active-directory-reporting-api-sign-in-activity-reference.md). 
* Als u wilt dat een volledig overzicht van het gebruik van toosee Hallo van Azure Active Directory rapportage-API, Zie [aan de slag met Azure Active Directory-rapportage API Hallo](active-directory-reporting-api-getting-started.md).
* Als u toofind voor meer informatie over Azure Active Directory-rapportage wilt, Zie Hallo [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).  


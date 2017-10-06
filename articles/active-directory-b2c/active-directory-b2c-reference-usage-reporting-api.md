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
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a>Toegang tot gebruiksrapporten in Azure AD B2C via Hallo rapportage-API

Azure Active Directory B2C (Azure AD B2C) biedt verificatie op basis van de gebruiker zich aanmelden en Azure multi-factor Authentication. Verificatie is bestemd voor eindgebruikers van uw toepassing familie over id-providers. Als u weet dat het aantal gebruikers die zijn geregistreerd in Hallo-tenant, ze gebruikt tooregister en het aantal authenticaties Hallo Hallo-providers per type Hallo kunt u beantwoorden van vragen als:
* Hoeveel gebruikers vanuit elk type id-provider (bijvoorbeeld een account van Microsoft of LinkedIn) hebt geregistreerd in het Hallo laatste 10 dagen?
* Het aantal authenticaties met multi-factor Authentication zijn in de afgelopen maand Hallo met succes voltooid?
* Hoeveel aanmelding in gebaseerd verificaties zijn deze maand voltooid? Per dag? Per toepassing?
* Hoe kan ik schatten Hallo verwachte maandelijkse kosten van de activiteit van mijn Azure AD B2C-tenant?

Dit artikel is gericht op de activiteit toobilling rapporten die zijn gekoppeld, die is gebaseerd op Hallo aantal gebruikers, factureerbare aanmelding in gebaseerd verificaties en multi-factor Authentication-oproepen.


## <a name="prerequisites"></a>Vereisten
Voordat u begint, moet u toocomplete Hallo stappen in [vereisten tooaccess hello Azure AD-rapportage API's](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/). Maken van een toepassing, een geheim voor het verkrijgen en verleen deze toegang hebben tot rechten tooyour Azure AD B2C-tenant-rapporten. *Script Bash* en *pythonscript* voorbeelden vindt u ook hier. 

## <a name="powershell-script"></a>PowerShell-script
Dit script wordt getoond hoe u Hallo vier gebruiksrapporten via Hallo `TimeStamp` parameter en Hallo `ApplicationId` filter.

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


## <a name="usage-report-definitions"></a>Gebruik rapportdefinities
* **tenantUserCount**: aantal gebruikers in de tenant door type id-provider per dag in Hallo HALLO hallo afgelopen 30 dagen. (U kunt desgewenst een `TimeStamp` -filter biedt gebruiker tellingen van een opgegeven datum toohello huidige datum). Hallo rapport biedt:
  * **TotalUserCount**: nummer van alle gebruikersobjecten Hallo.
  * **OtherUserCount**: Hallo aantal Azure Active Directory-gebruikers (geen Azure AD B2C-gebruikers).
  * **LocalUserCount**: Hallo aantal Azure AD B2C-gebruikersaccounts met referenties lokale toohello Azure AD B2C-tenant is gemaakt.

* **AlternateIdUserCount**: aantal gebruikers van Azure AD B2C Hallo geregistreerd bij de externe id-providers (bijvoorbeeld, Facebook, een Microsoft-account of een andere Azure Active Directory-tenant, ook wel aangeduid tooas een `OrgId`).

* **b2cAuthenticationCountSummary**: samenvatting van Hallo dagelijks aantal factureerbare verificaties via Hallo afgelopen 30 dagen door de dag en het type verificatiestroom.

* **b2cAuthenticationCount**: aantal verificaties Hallo binnen een periode. Hallo standaardwaarde is Hallo afgelopen 30 dagen.  (Optioneel: Hallo begin en eind `TimeStamp` parameters definiëren een specifiek tijdstip periode.) Hallo uitvoer bevat `StartTimeStamp` (vroegste datum van activiteiten voor deze tenant) en `EndTimeStamp` (laatste update).

* **b2cMfaRequestCountSummary**: samenvatting van Hallo dagelijks aantal multi-factor Authentication-oproepen per dag en het type (SMS of stem).


## <a name="limitations"></a>Beperkingen
Aantal gebruikersgegevens wordt elke 24 uur voor too48 vernieuwd. Authenticaties worden meerdere keren per dag bijgewerkt. Wanneer u Hallo `ApplicationId` filter, een antwoord leeg rapport kan worden veroorzaakt door tooone van de volgende voorwaarden:
  * Hallo toepassings-ID bestaat niet in Hallo-tenant. Zorg ervoor dat deze juist is.
  * Hallo toepassings-ID bestaat, maar er zijn geen gegevens gevonden in Hallo rapportageperiode. Herzie de datum/tijd-parameters.


## <a name="next-steps"></a>Volgende stappen
### <a name="monthly-bill-estimates-for-azure-ad"></a>Maandelijkse factuur schattingen voor Azure AD
In combinatie met [Hallo meest recente prijzen beschikbaar Azure AD B2C](https://azure.microsoft.com/pricing/details/active-directory-b2c/), u kunt schatten dagelijkse, wekelijkse en maandelijkse Azure-verbruik.  Een schatting is vooral nuttig wanneer u van plan bent om wijzigingen in gedrag die voor de totale kosten gevolgen mogelijk van de tenant. U kunt bekijken werkelijke kosten in uw [Azure-abonnement gekoppeld](active-directory-b2c-how-to-enable-billing.md).

### <a name="options-for-other-output-formats"></a>Opties voor andere uitvoerindelingen
Hallo ziet volgende code u voorbeelden van het verzenden van uitvoer tooJSON, een lijst met waarden van naam en XML:
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```

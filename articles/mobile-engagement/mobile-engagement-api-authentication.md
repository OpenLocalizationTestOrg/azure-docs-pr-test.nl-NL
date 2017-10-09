---
title: aaaAuthenticate met Mobile Engagement REST-API 's
description: Hierin wordt beschreven hoe tooauthenticate met Azure Mobile Engagement REST API's
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a>Verifiëren met Mobile Engagement REST-API 's
## <a name="overview"></a>Overzicht
Dit document beschrijft hoe een geldige AAD Oauth tooget token tooauthenticate Hello Mobile Engagement REST-API's. 

Er wordt van uitgegaan dat u een geldige Azure-abonnement hebt en u hebt gemaakt dat een Mobile Engagement-app met een van onze [Developer zelfstudies](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="authentication"></a>Authentication
OAuth-token wordt gebruikt voor verificatie op basis van een Microsoft Azure Active Directory. 

In de volgorde tooauthentication een API-aanvraag, moet de autorisatie-header worden toegevoegd aan tooevery aanvraag Hallo formulier te volgen:

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> Azure Active Directory-tokens verloopt over 1 uur.
> 
> 

Er zijn verschillende manieren tooget een token. Sinds Hallo die API 's in het algemeen worden aangeroepen vanuit een cloudservice, wilt u toouse een API-sleutel. Een API-sleutel in de Azure-terminologie heet een Service-principal wachtwoord. Hallo volgende procedure wordt beschreven eenrichtingssessie toosetting deze handmatig omhoog.

### <a name="one-time-setup-using-script"></a>Eenmalige instelling (met behulp van script)
U moet volgen Hallo reeks instructies hieronder tooperform hello geïnstalleerd met een PowerShell-script die Hallo minimale enige tijd vergt om setup, maar Hallo meest toegestane standaardwaarden gebruikt. Eventueel, u kunt ook instructies Hallo in Hallo [handmatige installatie](mobile-engagement-api-authentication-manual.md) om dit te doen van Hallo rechtstreeks Azure portal en de mate configuratie komen. 

1. Ophalen van de meest recente versie van Azure PowerShell van Hallo [hier](http://aka.ms/webpi-azps). Voor meer informatie over de downloadinstructies Hallo, u kunt dit zien [koppeling](/powershell/azure/overview).  
2. Wanneer Azure PowerShell is geïnstalleerd, gebruik Hallo volgende tooensure dat u Hallo hebt opdrachten **Azure-module** geïnstalleerd:
   
    a. Zorg ervoor dat hello Azure PowerShell-module is beschikbaar in Hallo lijst met beschikbare modules. 
   
        Get-Module –ListAvailable 
   
    ![Beschikbare Azure Modules][1]
   
    b. Als u hello Azure PowerShell-module niet in Hallo boven lijst vinden moet u toorun Hallo volgende:
   
        Import-Module Azure 
3. Aanmelding toohello Azure Resource Manager vanuit PowerShell door te voeren Hallo de volgende opdracht en het geven van uw gebruikersnaam en wachtwoord voor uw Azure-account: 
   
        Login-AzureRmAccount
4. Als u meerdere abonnementen hebt moet u de volgende Hallo uitvoeren:
   
    a. Een lijst van alle abonnementen en kopiëren Hallo abonnements-id van het Hallo-abonnement die u wilt dat toouse ophalen. Zorg ervoor dat dit abonnement is dezelfde waarvan Mobile Engagement-App die u gaat Hallo Hallo toointeract met het gebruik van Hallo API's. 
   
        Get-AzureRmSubscription
   
    b. Voer Hallo volgende opdracht met Hallo SubscriptionId tooconfigure Hallo abonnement toobe gebruikt.
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. Kopieer de tekst hello voor Hallo [nieuw AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) tooyour lokale machine script en sla deze op als een PowerShell-cmdlet (bijvoorbeeld `APIAuth.ps1`) en voer het `.\APIAuth.ps1`. 
6. Hallo script wordt u gevraagd tooprovide een invoer voor **primaire naam**. Geef een geschikte naam hier dat u toouse toocreate uw Active Directory-toepassing (bijvoorbeeld APIAuth wilt). 
7. Nadat het Hallo-script is voltooid, wordt deze weergegeven Hallo na vier waarden die u moet dus zorg ervoor dat toocopy tooauthenticate programmatisch met AD ze. 
   
    **TenantId**, **SubscriptionId**, **ApplicationId**, en **geheim**.
   
    U gebruikt TenantId als `{TENANT_ID}`, ApplicationId als `{CLIENT_ID}` en de geheime als `{CLIENT_SECRET}`.
   
   > [!NOTE]
   > Het beveiligingsbeleid van uw standaard blokkeren u een PowerShell-scripts worden uitgevoerd. Zo ja, configureren u tijdelijk de uitvoering van beleid tooallow uitvoering van het script met behulp van de volgende opdracht Hallo:
   > 
   > Set-ExecutionPolicy RemoteSigned
   > 
   > 
8. Hier ziet u hoe Hallo set cmdlets PS eruit zou zien. 
   
    ![][3]
9. Controleer in hello Azure Management portal of een nieuw AD-toepassing is gemaakt met de naam van de Hallo u opgegeven toohello script aangeroepen **primaire naam** onder **weergeven toepassingen mijn bedrijf eigenaar is van**.
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a>Stappen tooget een geldig token
1. Hallo-API aanroepen met de volgende parameters Hallo en zorg ervoor dat tooreplace hello TENANT\_-ID, CLIENT\_-ID en CLIENT\_GEHEIM:
   
   * **Aanvraag-URL** als *https://login.microsoftonline.com/ {TENANT\_ID} / oauth2/token*
   * **HTTP Content-Type-header** als *toepassing/x-1-800-www-Dell-form-urlencoded*
   * **HTTP-aanvraagtekst** als *verlenen\_type = client\_referenties & client_id = {CLIENT\_ID} & client_secret = {CLIENT\_GEHEIM} & resource=https%3A%2F%2Fmanagement.core.windows.net%2F*
     
     Hallo Hier volgt een voorbeeld van aanvraag:
     
       POST / {TENANT_ID} / oauth2/token HTTP/1.1-Host: login.microsoftonline.com Content-Type: application/x-1-800-www-Dell-form-urlencoded grant_type = client_credentials & client_id = {CLIENT_ID} & client_secret = {CLIENT_SECRET} & reso urce=https%3A%2F%2Fmanagement.core.windows.net%2F
     
     Hier volgt een voorbeeld van antwoord:
     
       HTTP/1.1 200 OK Content-Type: application/json; charset = utf-8-Content-Length: 1234
     
       {{'token_type': 'Bearer', 'expires_in': '3599', 'expires_on': '1445395811', 'not_before': ' 144 5391911 "," resource ': 'https://management.core.windows.net/', "access_token": {ACCESS_TOKEN}}
     
     In dit voorbeeld opgenomen URL-codering van Hallo POST-parameters, `resource` waarde is `https://management.core.windows.net/`. Wees voorzichtig tooalso URL-codering `{CLIENT_SECRET}` als deze speciale tekens mag bevatten.
     
     > [!NOTE]
     > Voor het testen, kunt u een HTTP-clienthulpprogramma zoals [Fiddler](http://www.telerik.com/fiddler) of [Postman Chrome-uitbreiding](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop) 
     > 
     > 
2. Omvatten nu in elke API-aanroep Hallo autorisatie aanvraag-header:
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    Als u een 401-statuscode geretourneerd, selectievakje Hallo antwoordtekst krijgt, dit kan erop wijzen dat Hallo-token is verlopen. In dat geval een nieuw token ophalen.

## <a name="using-hello-apis"></a>Hallo API's gebruiken
Nu dat u een ongeldig token hebt, bent u klaar toomake Hallo API-aanroepen.

1. Elke API-aanvraag moet u een geldige, niet-verlopen token dat u hebt verkregen in de vorige sectie Hallo toopass.
2. U moet tooplug in sommige parameters in Hallo aanvraag-URI die uw toepassing te identificeren. Hallo aanvraag-URI ziet eruit als Hallo volgende
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    tooget Hallo-parameters, klikt u op de toepassingsnaam van uw en klik op Dashboard en wordt er een pagina zoals Hallo volgende met alle Hallo 3 parameters.
   
   * **1** `{subscription-id}`
   * **2** `{app-collection}`
   * **3** `{app-resource-name}`
   * **4** gaat uw Resourcegroepnaam toobe **MobileEngagement** tenzij u een nieuw gemaakt. 
     
     ![Mobile Engagement API URI parameters][2]

> [!NOTE]
> <br/>
> 
> 1. Hallo API hoofdmap adres negeren omdat dit voor Hallo is vorige API's.<br/>
> 2. Als u Hallo-app met behulp van de klassieke Azure-portal gemaakt moet u toouse Hallo toepassing resourcenaam dit anders dan de naam van de toepassing hello zelf is. Als u Hallo app in Azure Portal Hallo gemaakt moet u Hallo de naam van de App zelf (Er is geen onderscheid tussen resourcenaam toepassing en de naam van de App voor apps die zijn gemaakt in de nieuwe portal Hallo) gebruiken.  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png




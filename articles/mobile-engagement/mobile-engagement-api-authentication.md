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
# <a name="authenticate-with-mobile-engagement-rest-apis"></a><span data-ttu-id="61351-103">Verifiëren met Mobile Engagement REST-API 's</span><span class="sxs-lookup"><span data-stu-id="61351-103">Authenticate with Mobile Engagement REST APIs</span></span>
## <a name="overview"></a><span data-ttu-id="61351-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="61351-104">Overview</span></span>
<span data-ttu-id="61351-105">Dit document beschrijft hoe een geldige AAD Oauth tooget token tooauthenticate Hello Mobile Engagement REST-API's.</span><span class="sxs-lookup"><span data-stu-id="61351-105">This document describes how tooget a valid AAD Oauth token tooauthenticate with hello Mobile Engagement REST APIs.</span></span> 

<span data-ttu-id="61351-106">Er wordt van uitgegaan dat u een geldige Azure-abonnement hebt en u hebt gemaakt dat een Mobile Engagement-app met een van onze [Developer zelfstudies](mobile-engagement-windows-store-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="61351-106">It is assumed that you have a valid Azure subscription and you have created a Mobile Engagement app using one of our [Developer Tutorials](mobile-engagement-windows-store-dotnet-get-started.md).</span></span>

## <a name="authentication"></a><span data-ttu-id="61351-107">Authentication</span><span class="sxs-lookup"><span data-stu-id="61351-107">Authentication</span></span>
<span data-ttu-id="61351-108">OAuth-token wordt gebruikt voor verificatie op basis van een Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="61351-108">A Microsoft Azure Active Directory based OAuth token is used for authentication.</span></span> 

<span data-ttu-id="61351-109">In de volgorde tooauthentication een API-aanvraag, moet de autorisatie-header worden toegevoegd aan tooevery aanvraag Hallo formulier te volgen:</span><span class="sxs-lookup"><span data-stu-id="61351-109">In order tooauthentication an API request, an authorization header must be added tooevery request which is of hello following form:</span></span>

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> <span data-ttu-id="61351-110">Azure Active Directory-tokens verloopt over 1 uur.</span><span class="sxs-lookup"><span data-stu-id="61351-110">Azure Active Directory tokens expire in 1 hour.</span></span>
> 
> 

<span data-ttu-id="61351-111">Er zijn verschillende manieren tooget een token.</span><span class="sxs-lookup"><span data-stu-id="61351-111">There are several ways tooget a token.</span></span> <span data-ttu-id="61351-112">Sinds Hallo die API 's in het algemeen worden aangeroepen vanuit een cloudservice, wilt u toouse een API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="61351-112">Since hello APIs are generally called from a cloud service, you want toouse an API key.</span></span> <span data-ttu-id="61351-113">Een API-sleutel in de Azure-terminologie heet een Service-principal wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="61351-113">An API key in Azure terminology is called a Service principal password.</span></span> <span data-ttu-id="61351-114">Hallo volgende procedure wordt beschreven eenrichtingssessie toosetting deze handmatig omhoog.</span><span class="sxs-lookup"><span data-stu-id="61351-114">hello following procedure describes one way toosetting it up manually.</span></span>

### <a name="one-time-setup-using-script"></a><span data-ttu-id="61351-115">Eenmalige instelling (met behulp van script)</span><span class="sxs-lookup"><span data-stu-id="61351-115">One-time setup (using script)</span></span>
<span data-ttu-id="61351-116">U moet volgen Hallo reeks instructies hieronder tooperform hello geïnstalleerd met een PowerShell-script die Hallo minimale enige tijd vergt om setup, maar Hallo meest toegestane standaardwaarden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="61351-116">You should follow hello set of instructions below tooperform hello setup using a PowerShell script which takes hello minimum time for setup but uses hello most permissible defaults.</span></span> <span data-ttu-id="61351-117">Eventueel, u kunt ook instructies Hallo in Hallo [handmatige installatie](mobile-engagement-api-authentication-manual.md) om dit te doen van Hallo rechtstreeks Azure portal en de mate configuratie komen.</span><span class="sxs-lookup"><span data-stu-id="61351-117">Optionally, you can also follow hello instructions in hello [manual setup](mobile-engagement-api-authentication-manual.md) for doing this from hello Azure portal directly and do finer configuration.</span></span> 

1. <span data-ttu-id="61351-118">Ophalen van de meest recente versie van Azure PowerShell van Hallo [hier](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="61351-118">Get hello latest version of Azure PowerShell from [here](http://aka.ms/webpi-azps).</span></span> <span data-ttu-id="61351-119">Voor meer informatie over de downloadinstructies Hallo, u kunt dit zien [koppeling](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61351-119">For more information on hello download instructions, you can see this [link](/powershell/azure/overview).</span></span>  
2. <span data-ttu-id="61351-120">Wanneer Azure PowerShell is geïnstalleerd, gebruik Hallo volgende tooensure dat u Hallo hebt opdrachten **Azure-module** geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="61351-120">Once Azure PowerShell is installed, use hello following commands tooensure that you have hello **Azure module** installed:</span></span>
   
    <span data-ttu-id="61351-121">a.</span><span class="sxs-lookup"><span data-stu-id="61351-121">a.</span></span> <span data-ttu-id="61351-122">Zorg ervoor dat hello Azure PowerShell-module is beschikbaar in Hallo lijst met beschikbare modules.</span><span class="sxs-lookup"><span data-stu-id="61351-122">Make sure hello Azure PowerShell module is available in hello list of available modules.</span></span> 
   
        Get-Module –ListAvailable 
   
    ![Beschikbare Azure Modules][1]
   
    <span data-ttu-id="61351-124">b.</span><span class="sxs-lookup"><span data-stu-id="61351-124">b.</span></span> <span data-ttu-id="61351-125">Als u hello Azure PowerShell-module niet in Hallo boven lijst vinden moet u toorun Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="61351-125">If you do not find hello Azure PowerShell module in hello above list then you need toorun hello following:</span></span>
   
        Import-Module Azure 
3. <span data-ttu-id="61351-126">Aanmelding toohello Azure Resource Manager vanuit PowerShell door te voeren Hallo de volgende opdracht en het geven van uw gebruikersnaam en wachtwoord voor uw Azure-account:</span><span class="sxs-lookup"><span data-stu-id="61351-126">Login toohello Azure Resource Manager from PowerShell by running hello following command and providing your user name and password for your Azure account:</span></span> 
   
        Login-AzureRmAccount
4. <span data-ttu-id="61351-127">Als u meerdere abonnementen hebt moet u de volgende Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="61351-127">If you have multiple subscriptions then you should run hello following:</span></span>
   
    <span data-ttu-id="61351-128">a.</span><span class="sxs-lookup"><span data-stu-id="61351-128">a.</span></span> <span data-ttu-id="61351-129">Een lijst van alle abonnementen en kopiëren Hallo abonnements-id van het Hallo-abonnement die u wilt dat toouse ophalen.</span><span class="sxs-lookup"><span data-stu-id="61351-129">Get a list of all your subscriptions and copy hello SubscriptionId of hello subscription you want toouse.</span></span> <span data-ttu-id="61351-130">Zorg ervoor dat dit abonnement is dezelfde waarvan Mobile Engagement-App die u gaat Hallo Hallo toointeract met het gebruik van Hallo API's.</span><span class="sxs-lookup"><span data-stu-id="61351-130">Make sure this subscription is hello same one which has hello Mobile Engagement App which you are going toointeract with using hello APIs.</span></span> 
   
        Get-AzureRmSubscription
   
    <span data-ttu-id="61351-131">b.</span><span class="sxs-lookup"><span data-stu-id="61351-131">b.</span></span> <span data-ttu-id="61351-132">Voer Hallo volgende opdracht met Hallo SubscriptionId tooconfigure Hallo abonnement toobe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="61351-132">Run hello following command providing hello SubscriptionId tooconfigure hello subscription toobe used.</span></span>
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. <span data-ttu-id="61351-133">Kopieer de tekst hello voor Hallo [nieuw AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) tooyour lokale machine script en sla deze op als een PowerShell-cmdlet (bijvoorbeeld `APIAuth.ps1`) en voer het `.\APIAuth.ps1`.</span><span class="sxs-lookup"><span data-stu-id="61351-133">Copy hello text for hello [New-AzureRmServicePrincipalOwner.ps1](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) script tooyour local machine and save it as a PowerShell cmdlet (e.g. `APIAuth.ps1`) and execute it `.\APIAuth.ps1`.</span></span> 
6. <span data-ttu-id="61351-134">Hallo script wordt u gevraagd tooprovide een invoer voor **primaire naam**.</span><span class="sxs-lookup"><span data-stu-id="61351-134">hello script will ask you tooprovide an input for **principalName**.</span></span> <span data-ttu-id="61351-135">Geef een geschikte naam hier dat u toouse toocreate uw Active Directory-toepassing (bijvoorbeeld APIAuth wilt).</span><span class="sxs-lookup"><span data-stu-id="61351-135">Provide a suitable name here that you want toouse toocreate your Active Directory application (e.g. APIAuth).</span></span> 
7. <span data-ttu-id="61351-136">Nadat het Hallo-script is voltooid, wordt deze weergegeven Hallo na vier waarden die u moet dus zorg ervoor dat toocopy tooauthenticate programmatisch met AD ze.</span><span class="sxs-lookup"><span data-stu-id="61351-136">After hello script completes, it will display hello following four values that you will need tooauthenticate programmatically with AD so make sure toocopy them.</span></span> 
   
    <span data-ttu-id="61351-137">**TenantId**, **SubscriptionId**, **ApplicationId**, en **geheim**.</span><span class="sxs-lookup"><span data-stu-id="61351-137">**TenantId**, **SubscriptionId**, **ApplicationId**, and **Secret**.</span></span>
   
    <span data-ttu-id="61351-138">U gebruikt TenantId als `{TENANT_ID}`, ApplicationId als `{CLIENT_ID}` en de geheime als `{CLIENT_SECRET}`.</span><span class="sxs-lookup"><span data-stu-id="61351-138">You will use TenantId as `{TENANT_ID}`, ApplicationId as `{CLIENT_ID}` and Secret as `{CLIENT_SECRET}`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="61351-139">Het beveiligingsbeleid van uw standaard blokkeren u een PowerShell-scripts worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="61351-139">Your default security policy may block you from running a PowerShell scripts.</span></span> <span data-ttu-id="61351-140">Zo ja, configureren u tijdelijk de uitvoering van beleid tooallow uitvoering van het script met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="61351-140">If so, you temporarily configure your execution policy tooallow script execution using hello following command:</span></span>
   > 
   > <span data-ttu-id="61351-141">Set-ExecutionPolicy RemoteSigned</span><span class="sxs-lookup"><span data-stu-id="61351-141">Set-ExecutionPolicy RemoteSigned</span></span>
   > 
   > 
8. <span data-ttu-id="61351-142">Hier ziet u hoe Hallo set cmdlets PS eruit zou zien.</span><span class="sxs-lookup"><span data-stu-id="61351-142">Here is how hello set of PS cmdlets would look like.</span></span> 
   
    ![][3]
9. <span data-ttu-id="61351-143">Controleer in hello Azure Management portal of een nieuw AD-toepassing is gemaakt met de naam van de Hallo u opgegeven toohello script aangeroepen **primaire naam** onder **weergeven toepassingen mijn bedrijf eigenaar is van**.</span><span class="sxs-lookup"><span data-stu-id="61351-143">Check in hello Azure Management portal that a new AD application was created with hello name you provided toohello script called **principalName** under **Show Applications my company owns**.</span></span>
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a><span data-ttu-id="61351-144">Stappen tooget een geldig token</span><span class="sxs-lookup"><span data-stu-id="61351-144">Steps tooget a valid token</span></span>
1. <span data-ttu-id="61351-145">Hallo-API aanroepen met de volgende parameters Hallo en zorg ervoor dat tooreplace hello TENANT\_-ID, CLIENT\_-ID en CLIENT\_GEHEIM:</span><span class="sxs-lookup"><span data-stu-id="61351-145">Call hello API with hello following parameters and make sure tooreplace hello TENANT\_ID, CLIENT\_ID and CLIENT\_SECRET:</span></span>
   
   * <span data-ttu-id="61351-146">**Aanvraag-URL** als *https://login.microsoftonline.com/ {TENANT\_ID} / oauth2/token*</span><span class="sxs-lookup"><span data-stu-id="61351-146">**Request URL** as *https://login.microsoftonline.com/{TENANT\_ID}/oauth2/token*</span></span>
   * <span data-ttu-id="61351-147">**HTTP Content-Type-header** als *toepassing/x-1-800-www-Dell-form-urlencoded*</span><span class="sxs-lookup"><span data-stu-id="61351-147">**HTTP Content-Type header** as *application/x-www-form-urlencoded*</span></span>
   * <span data-ttu-id="61351-148">**HTTP-aanvraagtekst** als *verlenen\_type = client\_referenties & client_id = {CLIENT\_ID} & client_secret = {CLIENT\_GEHEIM} & resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span><span class="sxs-lookup"><span data-stu-id="61351-148">**HTTP Request Body** as *grant\_type=client\_credentials&client_id={CLIENT\_ID}&client_secret={CLIENT\_SECRET}&resource=https%3A%2F%2Fmanagement.core.windows.net%2F*</span></span>
     
     <span data-ttu-id="61351-149">Hallo Hier volgt een voorbeeld van aanvraag:</span><span class="sxs-lookup"><span data-stu-id="61351-149">hello following is an example request:</span></span>
     
       <span data-ttu-id="61351-150">POST / {TENANT_ID} / oauth2/token HTTP/1.1-Host: login.microsoftonline.com Content-Type: application/x-1-800-www-Dell-form-urlencoded grant_type = client_credentials & client_id = {CLIENT_ID} & client_secret = {CLIENT_SECRET} & reso urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span><span class="sxs-lookup"><span data-stu-id="61351-150">POST /{TENANT_ID}/oauth2/token HTTP/1.1   Host: login.microsoftonline.com   Content-Type: application/x-www-form-urlencoded   grant_type=client_credentials&client_id={CLIENT_ID}&client_secret={CLIENT_SECRET}&reso   urce=https%3A%2F%2Fmanagement.core.windows.net%2F</span></span>
     
     <span data-ttu-id="61351-151">Hier volgt een voorbeeld van antwoord:</span><span class="sxs-lookup"><span data-stu-id="61351-151">Here is an example response:</span></span>
     
       <span data-ttu-id="61351-152">HTTP/1.1 200 OK Content-Type: application/json; charset = utf-8-Content-Length: 1234</span><span class="sxs-lookup"><span data-stu-id="61351-152">HTTP/1.1 200 OK   Content-Type: application/json; charset=utf-8   Content-Length: 1234</span></span>
     
       <span data-ttu-id="61351-153">{{'token_type': 'Bearer', 'expires_in': '3599', 'expires_on': '1445395811', 'not_before': ' 144 5391911 "," resource ': 'https://management.core.windows.net/', "access_token": {ACCESS_TOKEN}}</span><span class="sxs-lookup"><span data-stu-id="61351-153">{"token_type":"Bearer","expires_in":"3599","expires_on":"1445395811","not_before":"144   5391911","resource":"https://management.core.windows.net/","access_token":{ACCESS_TOKEN}}</span></span>
     
     <span data-ttu-id="61351-154">In dit voorbeeld opgenomen URL-codering van Hallo POST-parameters, `resource` waarde is `https://management.core.windows.net/`.</span><span class="sxs-lookup"><span data-stu-id="61351-154">This example included URL encoding of hello POST parameters, `resource` value is actually `https://management.core.windows.net/`.</span></span> <span data-ttu-id="61351-155">Wees voorzichtig tooalso URL-codering `{CLIENT_SECRET}` als deze speciale tekens mag bevatten.</span><span class="sxs-lookup"><span data-stu-id="61351-155">Be careful tooalso URL encode `{CLIENT_SECRET}` as it may contain special characters.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="61351-156">Voor het testen, kunt u een HTTP-clienthulpprogramma zoals [Fiddler](http://www.telerik.com/fiddler) of [Postman Chrome-uitbreiding](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span><span class="sxs-lookup"><span data-stu-id="61351-156">For testing, you can use an HTTP client tool like [Fiddler](http://www.telerik.com/fiddler) or [Chrome Postman extension](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop)</span></span> 
     > 
     > 
2. <span data-ttu-id="61351-157">Omvatten nu in elke API-aanroep Hallo autorisatie aanvraag-header:</span><span class="sxs-lookup"><span data-stu-id="61351-157">Now in every API call, include hello authorization request header:</span></span>
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    <span data-ttu-id="61351-158">Als u een 401-statuscode geretourneerd, selectievakje Hallo antwoordtekst krijgt, dit kan erop wijzen dat Hallo-token is verlopen.</span><span class="sxs-lookup"><span data-stu-id="61351-158">If you get a 401 status code returned, check hello response body, it might tell you hello token is expired.</span></span> <span data-ttu-id="61351-159">In dat geval een nieuw token ophalen.</span><span class="sxs-lookup"><span data-stu-id="61351-159">In that case, get a new token.</span></span>

## <a name="using-hello-apis"></a><span data-ttu-id="61351-160">Hallo API's gebruiken</span><span class="sxs-lookup"><span data-stu-id="61351-160">Using hello APIs</span></span>
<span data-ttu-id="61351-161">Nu dat u een ongeldig token hebt, bent u klaar toomake Hallo API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="61351-161">Now that you have a valid token, you are ready toomake hello API calls.</span></span>

1. <span data-ttu-id="61351-162">Elke API-aanvraag moet u een geldige, niet-verlopen token dat u hebt verkregen in de vorige sectie Hallo toopass.</span><span class="sxs-lookup"><span data-stu-id="61351-162">In each API request, you will need toopass a valid, unexpired token which you obtained in hello previous section.</span></span>
2. <span data-ttu-id="61351-163">U moet tooplug in sommige parameters in Hallo aanvraag-URI die uw toepassing te identificeren.</span><span class="sxs-lookup"><span data-stu-id="61351-163">You will need tooplug in some parameters into hello request URI which identifies your application.</span></span> <span data-ttu-id="61351-164">Hallo aanvraag-URI ziet eruit als Hallo volgende</span><span class="sxs-lookup"><span data-stu-id="61351-164">hello request URI looks like hello following</span></span>
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    <span data-ttu-id="61351-165">tooget Hallo-parameters, klikt u op de toepassingsnaam van uw en klik op Dashboard en wordt er een pagina zoals Hallo volgende met alle Hallo 3 parameters.</span><span class="sxs-lookup"><span data-stu-id="61351-165">tooget hello parameters, click on your application name and click Dashboard and you will see a page like hello following with all hello 3 parameters.</span></span>
   
   * <span data-ttu-id="61351-166">**1** `{subscription-id}`</span><span class="sxs-lookup"><span data-stu-id="61351-166">**1** `{subscription-id}`</span></span>
   * <span data-ttu-id="61351-167">**2** `{app-collection}`</span><span class="sxs-lookup"><span data-stu-id="61351-167">**2** `{app-collection}`</span></span>
   * <span data-ttu-id="61351-168">**3** `{app-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="61351-168">**3** `{app-resource-name}`</span></span>
   * <span data-ttu-id="61351-169">**4** gaat uw Resourcegroepnaam toobe **MobileEngagement** tenzij u een nieuw gemaakt.</span><span class="sxs-lookup"><span data-stu-id="61351-169">**4** Your Resource Group name is going toobe **MobileEngagement** unless you created a new one.</span></span> 
     
     ![Mobile Engagement API URI parameters][2]

> [!NOTE]
> <br/>
> 
> 1. <span data-ttu-id="61351-171">Hallo API hoofdmap adres negeren omdat dit voor Hallo is vorige API's.</span><span class="sxs-lookup"><span data-stu-id="61351-171">Ignore hello API Root Address as this was for hello previous APIs.</span></span><br/>
> 2. <span data-ttu-id="61351-172">Als u Hallo-app met behulp van de klassieke Azure-portal gemaakt moet u toouse Hallo toepassing resourcenaam dit anders dan de naam van de toepassing hello zelf is.</span><span class="sxs-lookup"><span data-stu-id="61351-172">If you created hello app using Azure Classic portal then you need toouse hello Application Resource name which is different than hello Application name itself.</span></span> <span data-ttu-id="61351-173">Als u Hallo app in Azure Portal Hallo gemaakt moet u Hallo de naam van de App zelf (Er is geen onderscheid tussen resourcenaam toepassing en de naam van de App voor apps die zijn gemaakt in de nieuwe portal Hallo) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="61351-173">If you created hello app in hello Azure Portal then you should use hello App Name itself (there is no differentiation between Application Resource Name and App Name for apps created in hello new portal).</span></span>  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png




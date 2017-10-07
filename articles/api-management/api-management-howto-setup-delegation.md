---
title: aaaHow toodelegate gebruiker registratie en de product-abonnement
description: Meer informatie over hoe toodelegate gebruiker registratie en product abonnement tooa derde partij in Azure API Management.
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a><span data-ttu-id="af3a6-103">Hoe toodelegate gebruiker registratie en de product-abonnement</span><span class="sxs-lookup"><span data-stu-id="af3a6-103">How toodelegate user registration and product subscription</span></span>
<span data-ttu-id="af3a6-104">Overdracht, kunt u toouse uw bestaande website voor het verwerken van ontwikkelaars sign-in/sign-up-to-date en abonnement tooproducts als toousing Hallo ingebouwde functionaliteit in de ontwikkelaarsportal Hallo geboden.</span><span class="sxs-lookup"><span data-stu-id="af3a6-104">Delegation allows you toouse your existing website for handling developer sign-in/sign-up and subscription tooproducts as opposed toousing hello built-in functionality in hello developer portal.</span></span> <span data-ttu-id="af3a6-105">Dit maakt het mogelijk uw website tooown Hallo gebruikergegevens en Hallo validatie van de volgende stappen uitvoeren in een aangepaste manier.</span><span class="sxs-lookup"><span data-stu-id="af3a6-105">This enables your website tooown hello user data and perform hello validation of these steps in a custom way.</span></span>

## <span data-ttu-id="af3a6-106"><a name="delegate-signin-up"></a>Overdragen developer aanmelden en registreren</span><span class="sxs-lookup"><span data-stu-id="af3a6-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="af3a6-107">toodelegate aanmelden en registreren tooyour bestaande website voor ontwikkelaars u een eindpunt speciale delegering toocreate op uw site die fungeert moet als toegangspunt voor het verzoek gestart vanaf Hallo API Management-portal voor ontwikkelaars Hallo.</span><span class="sxs-lookup"><span data-stu-id="af3a6-107">toodelegate developer sign-in and sign-up tooyour existing website you will need toocreate a special delegation endpoint on your site that acts as hello entry-point for any such request initiated from hello API Management developer portal.</span></span>

<span data-ttu-id="af3a6-108">Hallo laatste werkstroom zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="af3a6-108">hello final workflow will be as follows:</span></span>

1. <span data-ttu-id="af3a6-109">Ontwikkelaars klikt op Hallo aanmelden of registreren op koppeling Hallo API Management-portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="af3a6-109">Developer clicks on hello sign-in or sign-up link at hello API Management developer portal</span></span>
2. <span data-ttu-id="af3a6-110">Browser wordt omgeleid toohello delegering eindpunt</span><span class="sxs-lookup"><span data-stu-id="af3a6-110">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="af3a6-111">Eindpunt van de overdracht in leidt tooor geeft UI gevraagd gebruiker toosign in- of registreren</span><span class="sxs-lookup"><span data-stu-id="af3a6-111">Delegation endpoint in return redirects tooor presents UI asking user toosign-in or sign-up</span></span>
4. <span data-ttu-id="af3a6-112">Indien geslaagd kunt is Hallo gebruiker omgeleide back toohello API Management developer portal-pagina die ze vanuit gestart</span><span class="sxs-lookup"><span data-stu-id="af3a6-112">On success, hello user is redirected back toohello API Management developer portal page they started from</span></span>

<span data-ttu-id="af3a6-113">toobegin, gaan we eerste tooroute voor configuratie-API Management-aanvragen via uw eindpunt overdracht.</span><span class="sxs-lookup"><span data-stu-id="af3a6-113">toobegin, let's first set-up API Management tooroute requests via your delegation endpoint.</span></span> <span data-ttu-id="af3a6-114">Hallo publicatieportal van API Management, klik op **beveiliging** en klik vervolgens op Hallo **delegering** tabblad. Klik op Hallo selectievakje tooenable gemachtigde aanmelden en registreren.</span><span class="sxs-lookup"><span data-stu-id="af3a6-114">In hello API Management publisher portal, click on **Security** and then click hello **Delegation** tab. Click hello checkbox tooenable 'Delegate sign-in & sign-up'.</span></span>

![Overdracht pagina][api-management-delegation-signin-up]

* <span data-ttu-id="af3a6-116">Bepaal wat Hallo-URL van uw eindpunt speciale delegering wordt en invoeren in Hallo **delegering eindpunt-URL** veld.</span><span class="sxs-lookup"><span data-stu-id="af3a6-116">Decide what hello URL of your special delegation endpoint will be and enter it in hello **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="af3a6-117">Binnen Hallo **delegering verificatiesleutel** veld Voer een geheim dat is gebruikt toocompute een tooyou opgegeven handtekening voor de verificatie-tooensure die aanvraag Hallo inderdaad afkomstig is van Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="af3a6-117">Within hello **Delegation authentication key** field enter a secret that will be used toocompute a signature provided tooyou for verification tooensure that hello request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="af3a6-118">U kunt klikken op Hallo **genereren** knop toohave API een willekeurig genereren van een sleutel voor u.</span><span class="sxs-lookup"><span data-stu-id="af3a6-118">You can click hello **generate** button toohave API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="af3a6-119">Nu u toocreate hello moet **delegering eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="af3a6-119">Now you need toocreate hello **delegation endpoint**.</span></span> <span data-ttu-id="af3a6-120">Tooperform heeft een aantal acties:</span><span class="sxs-lookup"><span data-stu-id="af3a6-120">It has tooperform a number of actions:</span></span>

1. <span data-ttu-id="af3a6-121">Een aanvraag ontvangt in Hallo formulier te volgen:</span><span class="sxs-lookup"><span data-stu-id="af3a6-121">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="af3a6-122">*http://www.yourwebsite.com/apimdelegation?Operation=Signin&returnUrl= {URL van bronpagina} & salt = {tekenreeks} & sig = {tekenreeks}*</span><span class="sxs-lookup"><span data-stu-id="af3a6-122">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="af3a6-123">De queryparameters voor Hallo-in- / registratie-aanvraag:</span><span class="sxs-lookup"><span data-stu-id="af3a6-123">Query parameters for hello sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="af3a6-124">**bewerking**: welk type overdracht aanvraag is - deze kan alleen worden identificeert **SignIn** in dit geval</span><span class="sxs-lookup"><span data-stu-id="af3a6-124">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="af3a6-125">**returnUrl**: Hallo URL van Hallo pagina waar Hallo gebruiker hebt geklikt op een koppeling aanmelden of registreren</span><span class="sxs-lookup"><span data-stu-id="af3a6-125">**returnUrl**: hello URL of hello page where hello user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="af3a6-126">**Salt**: een speciale salt tekenreeks voor een hash beveiliging computing</span><span class="sxs-lookup"><span data-stu-id="af3a6-126">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="af3a6-127">**SIG**: een berekende beveiliging hash toobe gebruikt voor de vergelijking tooyour eigen berekende hash</span><span class="sxs-lookup"><span data-stu-id="af3a6-127">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="af3a6-128">Controleer of dat deze Hallo-aanvraag afkomstig is van Azure API Management (optioneel, maar sterk aanbevolen voor beveiliging)</span><span class="sxs-lookup"><span data-stu-id="af3a6-128">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="af3a6-129">Een HMAC SHA512-hash van een tekenreeks op basis van Hallo COMPUTE **returnUrl** en **salt** queryparameters ([voorbeeldcode hieronder]):</span><span class="sxs-lookup"><span data-stu-id="af3a6-129">Compute an HMAC-SHA512 hash of a string based on hello **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="af3a6-130">HMAC (**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="af3a6-130">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="af3a6-131">Vergelijk Hallo hierboven berekende hash toohello waarde Hallo **sig** queryparameter.</span><span class="sxs-lookup"><span data-stu-id="af3a6-131">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="af3a6-132">Als twee Hallo-hashes overeenkomen, op de volgende stap toohello verplaatst, anders dat Hallo-aanvraag wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="af3a6-132">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="af3a6-133">Controleer of u een aanvraag voor sign-in/aanmelding-up worden ontvangen: Hallo **bewerking** queryparameter te worden ingesteld '**SignIn**'.</span><span class="sxs-lookup"><span data-stu-id="af3a6-133">Verify that you are receiving a request for sign-in/sign-up: hello **operation** query parameter will be set too"**SignIn**".</span></span>
4. <span data-ttu-id="af3a6-134">Hallo gebruiker opleveren UI toosign in- of registreren</span><span class="sxs-lookup"><span data-stu-id="af3a6-134">Present hello user with UI toosign-in or sign-up</span></span>
5. <span data-ttu-id="af3a6-135">Als de gebruiker Hallo aanmelding hebt u toocreate een bijbehorende account voor hen in API Management.</span><span class="sxs-lookup"><span data-stu-id="af3a6-135">If hello user is signing-up you have toocreate a corresponding account for them in API Management.</span></span> <span data-ttu-id="af3a6-136">[Maken van een gebruiker] Hello API Management REST-API.</span><span class="sxs-lookup"><span data-stu-id="af3a6-136">[Create a user] with hello API Management REST API.</span></span> <span data-ttu-id="af3a6-137">Wanneer doet, moet u instellen van Hallo gebruiker-ID toohello tooan-ID die u kunt bijhouden van of hetzelfde in uw archief van de gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="af3a6-137">When doing so, ensure that you set hello user ID toohello same it is in your user store or tooan ID that you can keep track of.</span></span>
6. <span data-ttu-id="af3a6-138">Wanneer Hallo is geverifieerd:</span><span class="sxs-lookup"><span data-stu-id="af3a6-138">When hello user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="af3a6-139">[eenmalige aanmelding (SSO)-token van een aanvraag] via Hallo API Management REST-API</span><span class="sxs-lookup"><span data-stu-id="af3a6-139">[request a single-sign-on (SSO) token] via hello API Management REST API</span></span>
   * <span data-ttu-id="af3a6-140">een returnUrl query parameter toohello SSO-URL die u hebt ontvangen van de bovenstaande Hallo API-aanroep toevoegen:</span><span class="sxs-lookup"><span data-stu-id="af3a6-140">append a returnUrl query parameter toohello SSO URL you have received from hello API call above:</span></span>
     
     > <span data-ttu-id="af3a6-141">bijvoorbeeld https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="af3a6-141">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="af3a6-142">Hallo gebruiker toohello hierboven geproduceerde URL omleiden</span><span class="sxs-lookup"><span data-stu-id="af3a6-142">redirect hello user toohello above produced URL</span></span>

<span data-ttu-id="af3a6-143">In aanvulling toohello **SignIn** bewerking, kunt u ook uitvoeren accountbeheer door Hallo vorige stappen te volgen en met behulp van een Hallo bewerkingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="af3a6-143">In addition toohello **SignIn** operation, you can also perform account management by following hello previous steps and using one of hello following operations.</span></span>

* <span data-ttu-id="af3a6-144">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="af3a6-144">**ChangePassword**</span></span>
* <span data-ttu-id="af3a6-145">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="af3a6-145">**ChangeProfile**</span></span>
* <span data-ttu-id="af3a6-146">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="af3a6-146">**CloseAccount**</span></span>

<span data-ttu-id="af3a6-147">U moet doorgeven Hallo queryparameters voor accountbeheerbewerkingen te volgen.</span><span class="sxs-lookup"><span data-stu-id="af3a6-147">You must pass hello following query parameters for account management operations.</span></span>

* <span data-ttu-id="af3a6-148">**bewerking**: identificeert welk type overdracht aanvraag (ChangePassword, ChangeProfile of CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="af3a6-148">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="af3a6-149">**userId**: Hallo gebruikers-id van Hallo account toomanage</span><span class="sxs-lookup"><span data-stu-id="af3a6-149">**userId**: hello user id of hello account toomanage</span></span>
* <span data-ttu-id="af3a6-150">**Salt**: een speciale salt tekenreeks voor een hash beveiliging computing</span><span class="sxs-lookup"><span data-stu-id="af3a6-150">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="af3a6-151">**SIG**: een berekende beveiliging hash toobe gebruikt voor de vergelijking tooyour eigen berekende hash</span><span class="sxs-lookup"><span data-stu-id="af3a6-151">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>

## <span data-ttu-id="af3a6-152"><a name="delegate-product-subscription"></a>Product abonnement overdragen</span><span class="sxs-lookup"><span data-stu-id="af3a6-152"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="af3a6-153">Product abonnement delegeren werkt op dezelfde manier toodelegating gebruiker aanmelden /-up.</span><span class="sxs-lookup"><span data-stu-id="af3a6-153">Delegating product subscription works similarly toodelegating user sign-in/-up.</span></span> <span data-ttu-id="af3a6-154">laatste werkstroom Hallo zou als volgt zijn:</span><span class="sxs-lookup"><span data-stu-id="af3a6-154">hello final workflow would be as follows:</span></span>

1. <span data-ttu-id="af3a6-155">Ontwikkelaar selecteert een product in Hallo API Management-portal voor ontwikkelaars en klikt op Hallo abonneren knop</span><span class="sxs-lookup"><span data-stu-id="af3a6-155">Developer selects a product in hello API Management developer portal and clicks on hello Subscribe button</span></span>
2. <span data-ttu-id="af3a6-156">Browser wordt omgeleid toohello delegering eindpunt</span><span class="sxs-lookup"><span data-stu-id="af3a6-156">Browser is redirected toohello delegation endpoint</span></span>
3. <span data-ttu-id="af3a6-157">Overdracht eindpunt vereist product abonnement stappen worden uitgevoerd - dit is tooyou en kan leiden tot omleiding tooanother pagina toorequest factureringsgegevens, extra vragen, of het opslaan van informatie Hallo en niet een gebruikersactie vereist</span><span class="sxs-lookup"><span data-stu-id="af3a6-157">Delegation endpoint performs required product subscription steps - this is up tooyou and may entail redirecting tooanother page toorequest billing information, asking additional questions, or simply storing hello information and not requiring any user action</span></span>

<span data-ttu-id="af3a6-158">tooenable hello functionaliteit op Hallo **delegering** pagina op **delegeren product abonnement**.</span><span class="sxs-lookup"><span data-stu-id="af3a6-158">tooenable hello functionality, on hello **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="af3a6-159">Verzeker u ervan Hallo delegering eindpunt voert Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="af3a6-159">Then ensure hello delegation endpoint performs hello following actions:</span></span>

1. <span data-ttu-id="af3a6-160">Een aanvraag ontvangt in Hallo formulier te volgen:</span><span class="sxs-lookup"><span data-stu-id="af3a6-160">Receive a request in hello following form:</span></span>
   
   > <span data-ttu-id="af3a6-161">*{bewerking} http://www.yourwebsite.com/apimdelegation?Operation= & productId = {product toosubscribe naar} & userId = {user aanvraag} & salt = {tekenreeks} & sig = {tekenreeks}*</span><span class="sxs-lookup"><span data-stu-id="af3a6-161">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product toosubscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="af3a6-162">De queryparameters voor Hallo product abonnement geval:</span><span class="sxs-lookup"><span data-stu-id="af3a6-162">Query parameters for hello product subscription case:</span></span>
   
   * <span data-ttu-id="af3a6-163">**bewerking**: identificeert welk type overdracht aanvraag is.</span><span class="sxs-lookup"><span data-stu-id="af3a6-163">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="af3a6-164">Voor het product abonnement zijn aanvragen Hallo geldige opties:</span><span class="sxs-lookup"><span data-stu-id="af3a6-164">For product subscription requests hello valid options are:</span></span>
     * <span data-ttu-id="af3a6-165">'Abonneren': een verzoek toosubscribe Hallo gebruiker tooa opgegeven product met opgegeven ID (Zie hieronder)</span><span class="sxs-lookup"><span data-stu-id="af3a6-165">"Subscribe": a request toosubscribe hello user tooa given product with provided ID (see below)</span></span>
     * <span data-ttu-id="af3a6-166">'Afmelden': een verzoek toounsubscribe een gebruiker vanuit een product</span><span class="sxs-lookup"><span data-stu-id="af3a6-166">"Unsubscribe": a request toounsubscribe a user from a product</span></span>
     * <span data-ttu-id="af3a6-167">'Vernieuwen': een verzoek toorenew een abonnement (bijvoorbeeld die kan verlopen)</span><span class="sxs-lookup"><span data-stu-id="af3a6-167">"Renew": a requst toorenew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="af3a6-168">**productId**: Hallo-ID van Hallo product Hallo gebruiker toosubscribe naar aangevraagd</span><span class="sxs-lookup"><span data-stu-id="af3a6-168">**productId**: hello ID of hello product hello user requested toosubscribe to</span></span>
   * <span data-ttu-id="af3a6-169">**userId**: Hallo-ID van Hallo gebruiker voor wie Hallo-aanvraag wordt gedaan</span><span class="sxs-lookup"><span data-stu-id="af3a6-169">**userId**: hello ID of hello user for whom hello request is made</span></span>
   * <span data-ttu-id="af3a6-170">**Salt**: een speciale salt tekenreeks voor een hash beveiliging computing</span><span class="sxs-lookup"><span data-stu-id="af3a6-170">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="af3a6-171">**SIG**: een berekende beveiliging hash toobe gebruikt voor de vergelijking tooyour eigen berekende hash</span><span class="sxs-lookup"><span data-stu-id="af3a6-171">**sig**: a computed security hash toobe used for comparison tooyour own computed hash</span></span>
2. <span data-ttu-id="af3a6-172">Controleer of dat deze Hallo-aanvraag afkomstig is van Azure API Management (optioneel, maar sterk aanbevolen voor beveiliging)</span><span class="sxs-lookup"><span data-stu-id="af3a6-172">Verify that hello request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="af3a6-173">Een HMAC-SHA512 van een tekenreeks op basis van Hallo COMPUTE **productId**, **userId** en **salt** queryparameters:</span><span class="sxs-lookup"><span data-stu-id="af3a6-173">Compute an HMAC-SHA512 of a string based on hello **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="af3a6-174">HMAC (**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="af3a6-174">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="af3a6-175">Vergelijk Hallo hierboven berekende hash toohello waarde Hallo **sig** queryparameter.</span><span class="sxs-lookup"><span data-stu-id="af3a6-175">Compare hello above-computed hash toohello value of hello **sig** query parameter.</span></span> <span data-ttu-id="af3a6-176">Als twee Hallo-hashes overeenkomen, op de volgende stap toohello verplaatst, anders dat Hallo-aanvraag wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="af3a6-176">If hello two hashes match, move on toohello next step, otherwise deny hello request.</span></span>
3. <span data-ttu-id="af3a6-177">De verwerking van een abonnement die op basis van Hallo type in de aangevraagde bewerking uitvoeren **bewerking** -bijvoorbeeld facturering, meer vragen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="af3a6-177">Perform any product subscription processing based on hello type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="af3a6-178">Abonneren op het met succes abonneren Hallo gebruiker toohello product op uw kant, Hallo gebruiker toohello API Management-product door [aanroepen Hallo REST-API voor het product abonnement].</span><span class="sxs-lookup"><span data-stu-id="af3a6-178">On successfully subscribing hello user toohello product on your side, subscribe hello user toohello API Management product by [calling hello REST API for product subscription].</span></span>

## <span data-ttu-id="af3a6-179"><a name="delegate-example-code"></a> Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="af3a6-179"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="af3a6-180">Deze voorbeelden tonen hoe code tootake hello *delegering validatiesleutel*, die is ingesteld in overdracht welkomstscherm van de publicatieportal hello, toocreate een HMAC die vervolgens toovalidate Hallo handtekening, aan te tonen Hallo geldigheid van Hallo gebruikt doorgegeven returnUrl.</span><span class="sxs-lookup"><span data-stu-id="af3a6-180">These code samples show how tootake hello *delegation validation key*, which is set in hello Delegation screen of hello publisher portal, toocreate a HMAC which is then used toovalidate hello signature, proving hello validity of hello passed returnUrl.</span></span> <span data-ttu-id="af3a6-181">Hallo dezelfde code voor Hallo productId en userId met kleine wijziging werkt.</span><span class="sxs-lookup"><span data-stu-id="af3a6-181">hello same code works for hello productId and userId with slight modification.</span></span>

<span data-ttu-id="af3a6-182">**C#-code toogenerate hash van returnUrl**</span><span class="sxs-lookup"><span data-stu-id="af3a6-182">**C# code toogenerate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

<span data-ttu-id="af3a6-183">**NodeJS code toogenerate hash van returnUrl**</span><span class="sxs-lookup"><span data-stu-id="af3a6-183">**NodeJS code toogenerate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="af3a6-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="af3a6-184">Next steps</span></span>
<span data-ttu-id="af3a6-185">Zie voor meer informatie over delegering Hallo video te volgen.</span><span class="sxs-lookup"><span data-stu-id="af3a6-185">For more information on delegation, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[eenmalige aanmelding (SSO)-token van een aanvraag]: http://go.microsoft.com/fwlink/?LinkId=507409
[een gebruiker maken]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[aanroepen Hallo REST-API voor het product abonnement]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[voorbeeldcode hieronder]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 

---
title: Het overdragen van de gebruiker de registratie- en productinformatie abonnement
description: Informatie over het overdragen van de registratie en product gebruikerabonnement aan een derde partij in Azure API Management.
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
ms.openlocfilehash: 2637ab6405f2d4ea1da84981295a144874dfa4f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-delegate-user-registration-and-product-subscription"></a><span data-ttu-id="1cb25-103">Het overdragen van de gebruiker de registratie- en productinformatie abonnement</span><span class="sxs-lookup"><span data-stu-id="1cb25-103">How to delegate user registration and product subscription</span></span>
<span data-ttu-id="1cb25-104">Overdracht kunt u uw bestaande website te gebruiken voor het verwerken van ontwikkelaars sign-in/sign-up-to-date en abonnement op producten in plaats van met behulp van de ingebouwde functie in de portal voor ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="1cb25-104">Delegation allows you to use your existing website for handling developer sign-in/sign-up and subscription to products as opposed to using the built-in functionality in the developer portal.</span></span> <span data-ttu-id="1cb25-105">Hierdoor kan uw website aan de eigenaar van de gebruikersgegevens en de validatie van de volgende stappen uitvoeren in een aangepaste manier.</span><span class="sxs-lookup"><span data-stu-id="1cb25-105">This enables your website to own the user data and perform the validation of these steps in a custom way.</span></span>

## <span data-ttu-id="1cb25-106"><a name="delegate-signin-up"></a>Overdragen developer aanmelden en registreren</span><span class="sxs-lookup"><span data-stu-id="1cb25-106"><a name="delegate-signin-up"> </a>Delegating developer sign-in and sign-up</span></span>
<span data-ttu-id="1cb25-107">Om te delegeren developer aanmelden en aanmelden met uw bestaande website, moet u een speciale delegering-eindpunt op de site die als het toegangspunt voor het verzoek gestart vanuit de ontwikkelaarsportal API Management fungeert maken.</span><span class="sxs-lookup"><span data-stu-id="1cb25-107">To delegate developer sign-in and sign-up to your existing website you will need to create a special delegation endpoint on your site that acts as the entry-point for any such request initiated from the API Management developer portal.</span></span>

<span data-ttu-id="1cb25-108">De laatste werkstroom zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="1cb25-108">The final workflow will be as follows:</span></span>

1. <span data-ttu-id="1cb25-109">Ontwikkelaars klikken op de koppeling aanmelden of registreren bij API Management-portal voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="1cb25-109">Developer clicks on the sign-in or sign-up link at the API Management developer portal</span></span>
2. <span data-ttu-id="1cb25-110">Browser wordt omgeleid naar het eindpunt voor overdracht</span><span class="sxs-lookup"><span data-stu-id="1cb25-110">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="1cb25-111">Eindpunt van de overdracht wordt omgeleid naar in of geeft UI gebruiker wordt gevraagd te aanmelden of registreren</span><span class="sxs-lookup"><span data-stu-id="1cb25-111">Delegation endpoint in return redirects to or presents UI asking user to sign-in or sign-up</span></span>
4. <span data-ttu-id="1cb25-112">Indien geslaagd kunt wordt de gebruiker omgeleid naar de API Management developer portal-pagina die ze vanaf gestart</span><span class="sxs-lookup"><span data-stu-id="1cb25-112">On success, the user is redirected back to the API Management developer portal page they started from</span></span>

<span data-ttu-id="1cb25-113">Om te beginnen, aanvragen laten we eerst set-up API Management te routeren via uw eindpunt overdracht.</span><span class="sxs-lookup"><span data-stu-id="1cb25-113">To begin, let's first set-up API Management to route requests via your delegation endpoint.</span></span> <span data-ttu-id="1cb25-114">Klik in de publicatieportal van API Management op **beveiliging** en klik vervolgens op de **delegering** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1cb25-114">In the API Management publisher portal, click on **Security** and then click the **Delegation** tab.</span></span> <span data-ttu-id="1cb25-115">Klik op het selectievakje in zodat de gemachtigde-in- en registratie.</span><span class="sxs-lookup"><span data-stu-id="1cb25-115">Click the checkbox to enable 'Delegate sign-in & sign-up'.</span></span>

![Overdracht pagina][api-management-delegation-signin-up]

* <span data-ttu-id="1cb25-117">Bepalen wat de URL van uw eindpunt speciale delegering wordt en voer deze in de **delegering eindpunt-URL** veld.</span><span class="sxs-lookup"><span data-stu-id="1cb25-117">Decide what the URL of your special delegation endpoint will be and enter it in the **Delegation endpoint URL** field.</span></span> 
* <span data-ttu-id="1cb25-118">Binnen de **delegering verificatiesleutel** veld Voer een geheim dat wordt gebruikt voor het berekenen van een handtekening die u voor verificatie om ervoor te zorgen dat de aanvraag inderdaad afkomstig is van Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="1cb25-118">Within the **Delegation authentication key** field enter a secret that will be used to compute a signature provided to you for verification to ensure that the request is indeed coming from Azure API Management.</span></span> <span data-ttu-id="1cb25-119">U kunt klikken op de **genereren** knop API een willekeurig genereren van een sleutel voor u hebben.</span><span class="sxs-lookup"><span data-stu-id="1cb25-119">You can click the **generate** button to have API Managemnet randomly generate a key for you.</span></span>

<span data-ttu-id="1cb25-120">Nu moet u maken de **delegering eindpunt**.</span><span class="sxs-lookup"><span data-stu-id="1cb25-120">Now you need to create the **delegation endpoint**.</span></span> <span data-ttu-id="1cb25-121">Er is een aantal acties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1cb25-121">It has to perform a number of actions:</span></span>

1. <span data-ttu-id="1cb25-122">Een aanvraag ontvangen in de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="1cb25-122">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="1cb25-123">*http://www.yourwebsite.com/apimdelegation?Operation=Signin&returnUrl= {URL van bronpagina} & salt = {tekenreeks} & sig = {tekenreeks}*</span><span class="sxs-lookup"><span data-stu-id="1cb25-123">*http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL of source page}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="1cb25-124">De queryparameters voor de aanvraag-in- / registratie:</span><span class="sxs-lookup"><span data-stu-id="1cb25-124">Query parameters for the sign-in / sign-up case:</span></span>
   
   * <span data-ttu-id="1cb25-125">**bewerking**: welk type overdracht aanvraag is - deze kan alleen worden identificeert **SignIn** in dit geval</span><span class="sxs-lookup"><span data-stu-id="1cb25-125">**operation**: identifies what type of delegation request it is - it can only be **SignIn** in this case</span></span>
   * <span data-ttu-id="1cb25-126">**returnUrl**: de URL van de pagina waar de gebruiker hebt geklikt op een koppeling aanmelden of registreren</span><span class="sxs-lookup"><span data-stu-id="1cb25-126">**returnUrl**: the URL of the page where the user clicked on a sign-in or sign-up link</span></span>
   * <span data-ttu-id="1cb25-127">**Salt**: een speciale salt tekenreeks voor een hash beveiliging computing</span><span class="sxs-lookup"><span data-stu-id="1cb25-127">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="1cb25-128">**SIG**: een hash van de berekende beveiliging moet worden gebruikt voor vergelijking van uw eigen berekende hash</span><span class="sxs-lookup"><span data-stu-id="1cb25-128">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="1cb25-129">Controleer of dat de aanvraag afkomstig is van Azure API Management (optioneel, maar sterk aanbevolen voor beveiliging)</span><span class="sxs-lookup"><span data-stu-id="1cb25-129">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="1cb25-130">COMPUTE een HMAC SHA512-hash van een tekenreeks op basis van de **returnUrl** en **salt** queryparameters ([voorbeeldcode hieronder]):</span><span class="sxs-lookup"><span data-stu-id="1cb25-130">Compute an HMAC-SHA512 hash of a string based on the **returnUrl** and **salt** query parameters ([example code provided below]):</span></span>
     
     > <span data-ttu-id="1cb25-131">HMAC (**salt** + '\n' + **returnUrl**)</span><span class="sxs-lookup"><span data-stu-id="1cb25-131">HMAC(**salt** + '\n' + **returnUrl**)</span></span>
     > 
     > 
   * <span data-ttu-id="1cb25-132">Vergelijk de bovenstaande berekende hash op de waarde van de **sig** queryparameter.</span><span class="sxs-lookup"><span data-stu-id="1cb25-132">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="1cb25-133">Als de twee hashes overeenkomen, gaat u verder met de volgende stap, anders dat de aanvraag wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="1cb25-133">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="1cb25-134">Controleer of u een aanvraag voor sign-in/aanmelding-up worden ontvangen: de **bewerking** queryparameter wordt ingesteld op '**SignIn**'.</span><span class="sxs-lookup"><span data-stu-id="1cb25-134">Verify that you are receiving a request for sign-in/sign-up: the **operation** query parameter will be set to "**SignIn**".</span></span>
4. <span data-ttu-id="1cb25-135">De gebruiker opleveren UI aanmelden of registreren</span><span class="sxs-lookup"><span data-stu-id="1cb25-135">Present the user with UI to sign-in or sign-up</span></span>
5. <span data-ttu-id="1cb25-136">Als de gebruiker de aanmelding is die u moet een bijbehorende account voor hen maken in API Management.</span><span class="sxs-lookup"><span data-stu-id="1cb25-136">If the user is signing-up you have to create a corresponding account for them in API Management.</span></span> <span data-ttu-id="1cb25-137">[Maken van een gebruiker] met de REST-API van API Management.</span><span class="sxs-lookup"><span data-stu-id="1cb25-137">[Create a user] with the API Management REST API.</span></span> <span data-ttu-id="1cb25-138">Wanneer doet, zorg ervoor dat u de gebruikers-ID ingesteld op hetzelfde is in uw archief van de gebruiker of een id die u kunt van bijhouden.</span><span class="sxs-lookup"><span data-stu-id="1cb25-138">When doing so, ensure that you set the user ID to the same it is in your user store or to an ID that you can keep track of.</span></span>
6. <span data-ttu-id="1cb25-139">Wanneer de gebruiker is geverifieerd:</span><span class="sxs-lookup"><span data-stu-id="1cb25-139">When the user is successfully authenticated:</span></span>
   
   * <span data-ttu-id="1cb25-140">[eenmalige aanmelding (SSO)-token van een aanvraag] via de API Management REST API</span><span class="sxs-lookup"><span data-stu-id="1cb25-140">[request a single-sign-on (SSO) token] via the API Management REST API</span></span>
   * <span data-ttu-id="1cb25-141">een queryparameter returnUrl toevoegen aan de SSO-URL die u hebt ontvangen van de API-aanroep hierboven:</span><span class="sxs-lookup"><span data-stu-id="1cb25-141">append a returnUrl query parameter to the SSO URL you have received from the API call above:</span></span>
     
     > <span data-ttu-id="1cb25-142">bijvoorbeeld https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span><span class="sxs-lookup"><span data-stu-id="1cb25-142">e.g. https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url</span></span> 
     > 
     > 
   * <span data-ttu-id="1cb25-143">de gebruiker omgeleid naar de URL van de bovenstaande geproduceerd</span><span class="sxs-lookup"><span data-stu-id="1cb25-143">redirect the user to the above produced URL</span></span>

<span data-ttu-id="1cb25-144">Naast de **SignIn** bewerking, kunt u ook uitvoeren accountbeheer door de vorige stappen te volgen en het gebruik van een van de volgende bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="1cb25-144">In addition to the **SignIn** operation, you can also perform account management by following the previous steps and using one of the following operations.</span></span>

* <span data-ttu-id="1cb25-145">**ChangePassword**</span><span class="sxs-lookup"><span data-stu-id="1cb25-145">**ChangePassword**</span></span>
* <span data-ttu-id="1cb25-146">**ChangeProfile**</span><span class="sxs-lookup"><span data-stu-id="1cb25-146">**ChangeProfile**</span></span>
* <span data-ttu-id="1cb25-147">**CloseAccount**</span><span class="sxs-lookup"><span data-stu-id="1cb25-147">**CloseAccount**</span></span>

<span data-ttu-id="1cb25-148">U moet de volgende queryparameters voor accountbeheerbewerkingen doorgeven.</span><span class="sxs-lookup"><span data-stu-id="1cb25-148">You must pass the following query parameters for account management operations.</span></span>

* <span data-ttu-id="1cb25-149">**bewerking**: identificeert welk type overdracht aanvraag (ChangePassword, ChangeProfile of CloseAccount)</span><span class="sxs-lookup"><span data-stu-id="1cb25-149">**operation**: identifies what type of delegation request it is (ChangePassword, ChangeProfile, or CloseAccount)</span></span>
* <span data-ttu-id="1cb25-150">**userId**: de gebruikers-id van het account voor het beheren van</span><span class="sxs-lookup"><span data-stu-id="1cb25-150">**userId**: the user id of the account to manage</span></span>
* <span data-ttu-id="1cb25-151">**Salt**: een speciale salt tekenreeks voor een hash beveiliging computing</span><span class="sxs-lookup"><span data-stu-id="1cb25-151">**salt**: a special salt string used for computing a security hash</span></span>
* <span data-ttu-id="1cb25-152">**SIG**: een hash van de berekende beveiliging moet worden gebruikt voor vergelijking van uw eigen berekende hash</span><span class="sxs-lookup"><span data-stu-id="1cb25-152">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>

## <span data-ttu-id="1cb25-153"><a name="delegate-product-subscription"></a>Product abonnement overdragen</span><span class="sxs-lookup"><span data-stu-id="1cb25-153"><a name="delegate-product-subscription"> </a>Delegating product subscription</span></span>
<span data-ttu-id="1cb25-154">Product abonnement delegeren werkt op dezelfde manier voor het delegeren van de gebruiker aanmelden /-up.</span><span class="sxs-lookup"><span data-stu-id="1cb25-154">Delegating product subscription works similarly to delegating user sign-in/-up.</span></span> <span data-ttu-id="1cb25-155">De laatste werkstroom zou als volgt zijn:</span><span class="sxs-lookup"><span data-stu-id="1cb25-155">The final workflow would be as follows:</span></span>

1. <span data-ttu-id="1cb25-156">Ontwikkelaar een product selecteert in de API Management-portal voor ontwikkelaars en klikt op de knop aanmelden</span><span class="sxs-lookup"><span data-stu-id="1cb25-156">Developer selects a product in the API Management developer portal and clicks on the Subscribe button</span></span>
2. <span data-ttu-id="1cb25-157">Browser wordt omgeleid naar het eindpunt voor overdracht</span><span class="sxs-lookup"><span data-stu-id="1cb25-157">Browser is redirected to the delegation endpoint</span></span>
3. <span data-ttu-id="1cb25-158">Overdracht eindpunt vereist product abonnement stappen worden uitgevoerd - deze bepaalt zelf en kan leiden tot omleiden naar een andere pagina om aan te vragen factureringsgegevens extra vragen, of het opslaan van de informatie en niet een gebruikersactie vereist</span><span class="sxs-lookup"><span data-stu-id="1cb25-158">Delegation endpoint performs required product subscription steps - this is up to you and may entail redirecting to another page to request billing information, asking additional questions, or simply storing the information and not requiring any user action</span></span>

<span data-ttu-id="1cb25-159">Voor het inschakelen van de functionaliteit op de **delegering** pagina op **delegeren product abonnement**.</span><span class="sxs-lookup"><span data-stu-id="1cb25-159">To enable the functionality, on the **Delegation** page click **Delegate product subscription**.</span></span>

<span data-ttu-id="1cb25-160">Verzeker u ervan dat het eindpunt van de overdracht worden de volgende acties uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="1cb25-160">Then ensure the delegation endpoint performs the following actions:</span></span>

1. <span data-ttu-id="1cb25-161">Een aanvraag ontvangen in de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="1cb25-161">Receive a request in the following form:</span></span>
   
   > <span data-ttu-id="1cb25-162">*{bewerking} http://www.yourwebsite.com/apimdelegation?Operation= & productId = {product abonneren op} & userId = {user aanvraag} & salt = {tekenreeks} & sig = {tekenreeks}*</span><span class="sxs-lookup"><span data-stu-id="1cb25-162">*http://www.yourwebsite.com/apimdelegation?operation={operation}&productId={product to subscribe to}&userId={user making request}&salt={string}&sig={string}*</span></span>
   > 
   > 
   
    <span data-ttu-id="1cb25-163">De queryparameters voor het product abonnement geval:</span><span class="sxs-lookup"><span data-stu-id="1cb25-163">Query parameters for the product subscription case:</span></span>
   
   * <span data-ttu-id="1cb25-164">**bewerking**: identificeert welk type overdracht aanvraag is.</span><span class="sxs-lookup"><span data-stu-id="1cb25-164">**operation**: identifies what type of delegation request it is.</span></span> <span data-ttu-id="1cb25-165">Voor het product abonnement zijn aanvragen de geldige opties:</span><span class="sxs-lookup"><span data-stu-id="1cb25-165">For product subscription requests the valid options are:</span></span>
     * <span data-ttu-id="1cb25-166">'Abonneren': een verzoek voor een abonnement van de gebruiker voor een bepaald product met opgegeven ID (Zie hieronder)</span><span class="sxs-lookup"><span data-stu-id="1cb25-166">"Subscribe": a request to subscribe the user to a given product with provided ID (see below)</span></span>
     * <span data-ttu-id="1cb25-167">'Afmelden': een verzoek om te stoppen van een gebruiker vanuit een product</span><span class="sxs-lookup"><span data-stu-id="1cb25-167">"Unsubscribe": a request to unsubscribe a user from a product</span></span>
     * <span data-ttu-id="1cb25-168">'Vernieuwen': een verzoek om een abonnement (bijvoorbeeld die kan verlopen) te vernieuwen</span><span class="sxs-lookup"><span data-stu-id="1cb25-168">"Renew": a requst to renew a subscription (e.g. that may be expiring)</span></span>
   * <span data-ttu-id="1cb25-169">**productId**: de ID van het product dat de gebruiker gevraagd om u te abonneren op</span><span class="sxs-lookup"><span data-stu-id="1cb25-169">**productId**: the ID of the product the user requested to subscribe to</span></span>
   * <span data-ttu-id="1cb25-170">**userId**: de ID van de gebruiker voor wie de aanvraag wordt gedaan</span><span class="sxs-lookup"><span data-stu-id="1cb25-170">**userId**: the ID of the user for whom the request is made</span></span>
   * <span data-ttu-id="1cb25-171">**Salt**: een speciale salt tekenreeks voor een hash beveiliging computing</span><span class="sxs-lookup"><span data-stu-id="1cb25-171">**salt**: a special salt string used for computing a security hash</span></span>
   * <span data-ttu-id="1cb25-172">**SIG**: een hash van de berekende beveiliging moet worden gebruikt voor vergelijking van uw eigen berekende hash</span><span class="sxs-lookup"><span data-stu-id="1cb25-172">**sig**: a computed security hash to be used for comparison to your own computed hash</span></span>
2. <span data-ttu-id="1cb25-173">Controleer of dat de aanvraag afkomstig is van Azure API Management (optioneel, maar sterk aanbevolen voor beveiliging)</span><span class="sxs-lookup"><span data-stu-id="1cb25-173">Verify that the request is coming from Azure API Management (optional, but highly recommended for security)</span></span>
   
   * <span data-ttu-id="1cb25-174">COMPUTE een HMAC-SHA512 van een tekenreeks op basis van de **productId**, **userId** en **salt** queryparameters:</span><span class="sxs-lookup"><span data-stu-id="1cb25-174">Compute an HMAC-SHA512 of a string based on the **productId**, **userId** and **salt** query parameters:</span></span>
     
     > <span data-ttu-id="1cb25-175">HMAC (**salt** + '\n' + **productId** + '\n' + **userId**)</span><span class="sxs-lookup"><span data-stu-id="1cb25-175">HMAC(**salt** + '\n' + **productId** + '\n' + **userId**)</span></span>
     > 
     > 
   * <span data-ttu-id="1cb25-176">Vergelijk de bovenstaande berekende hash op de waarde van de **sig** queryparameter.</span><span class="sxs-lookup"><span data-stu-id="1cb25-176">Compare the above-computed hash to the value of the **sig** query parameter.</span></span> <span data-ttu-id="1cb25-177">Als de twee hashes overeenkomen, gaat u verder met de volgende stap, anders dat de aanvraag wordt geweigerd.</span><span class="sxs-lookup"><span data-stu-id="1cb25-177">If the two hashes match, move on to the next step, otherwise deny the request.</span></span>
3. <span data-ttu-id="1cb25-178">De verwerking van een abonnement die op basis van het type in de aangevraagde bewerking uitvoeren **bewerking** -bijvoorbeeld facturering, meer vragen, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="1cb25-178">Perform any product subscription processing based on the type of operation requested in **operation** - e.g. billing, further questions, etc.</span></span>
4. <span data-ttu-id="1cb25-179">Abonneren op het abonnement is de gebruiker op het product aan uw kant, door de gebruiker het API Management-product door [aanroepen van de REST-API voor het product abonnement].</span><span class="sxs-lookup"><span data-stu-id="1cb25-179">On successfully subscribing the user to the product on your side, subscribe the user to the API Management product by [calling the REST API for product subscription].</span></span>

## <span data-ttu-id="1cb25-180"><a name="delegate-example-code"></a> Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="1cb25-180"><a name="delegate-example-code"> </a> Example Code</span></span>
<span data-ttu-id="1cb25-181">Deze codevoorbeelden laten zien hoe nemen de *delegering validatiesleutel*, die in het scherm van de overdracht van de publicatieportal is ingesteld voor het maken van een HMAC die vervolgens wordt gebruikt voor het valideren van de handtekening, de geldigheid van de returnUrl die is doorgegeven aan te tonen.</span><span class="sxs-lookup"><span data-stu-id="1cb25-181">These code samples show how to take the *delegation validation key*, which is set in the Delegation screen of the publisher portal, to create a HMAC which is then used to validate the signature, proving the validity of the passed returnUrl.</span></span> <span data-ttu-id="1cb25-182">De dezelfde code werkt voor de product-id en gebruikers-id met kleine wijziging.</span><span class="sxs-lookup"><span data-stu-id="1cb25-182">The same code works for the productId and userId with slight modification.</span></span>

<span data-ttu-id="1cb25-183">**C#-code voor het genereren van de hash van returnUrl**</span><span class="sxs-lookup"><span data-stu-id="1cb25-183">**C# code to generate hash of returnUrl**</span></span>

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature to sig query parameter
}
```

<span data-ttu-id="1cb25-184">**Code genereren van de hash van returnUrl NodeJS**</span><span class="sxs-lookup"><span data-stu-id="1cb25-184">**NodeJS code to generate hash of returnUrl**</span></span>

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change to (salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature to sig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a><span data-ttu-id="1cb25-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1cb25-185">Next steps</span></span>
<span data-ttu-id="1cb25-186">Zie de volgende video voor meer informatie over delegering.</span><span class="sxs-lookup"><span data-stu-id="1cb25-186">For more information on delegation, see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
<span data-ttu-id="1cb25-187">[eenmalige aanmelding (SSO)-token van een aanvraag]: http://go.microsoft.com/fwlink/?LinkId=507409</span><span class="sxs-lookup"><span data-stu-id="1cb25-187">[request a single-sign-on (SSO) token]: http://go.microsoft.com/fwlink/?LinkId=507409</span></span>
<span data-ttu-id="1cb25-188">[een gebruiker maken]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span><span class="sxs-lookup"><span data-stu-id="1cb25-188">[create a user]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser</span></span>
<span data-ttu-id="1cb25-189">[aanroepen van de REST-API voor het product abonnement]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span><span class="sxs-lookup"><span data-stu-id="1cb25-189">[calling the REST API for product subscription]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO</span></span>
[Next steps]: #next-steps
<span data-ttu-id="1cb25-190">[voorbeeldcode hieronder]: #delegate-example-code</span><span class="sxs-lookup"><span data-stu-id="1cb25-190">[example code provided below]: #delegate-example-code</span></span>

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 

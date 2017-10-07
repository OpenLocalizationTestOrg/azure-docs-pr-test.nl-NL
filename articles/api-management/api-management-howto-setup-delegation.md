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
# <a name="how-toodelegate-user-registration-and-product-subscription"></a>Hoe toodelegate gebruiker registratie en de product-abonnement
Overdracht, kunt u toouse uw bestaande website voor het verwerken van ontwikkelaars sign-in/sign-up-to-date en abonnement tooproducts als toousing Hallo ingebouwde functionaliteit in de ontwikkelaarsportal Hallo geboden. Dit maakt het mogelijk uw website tooown Hallo gebruikergegevens en Hallo validatie van de volgende stappen uitvoeren in een aangepaste manier.

## <a name="delegate-signin-up"></a>Overdragen developer aanmelden en registreren
toodelegate aanmelden en registreren tooyour bestaande website voor ontwikkelaars u een eindpunt speciale delegering toocreate op uw site die fungeert moet als toegangspunt voor het verzoek gestart vanaf Hallo API Management-portal voor ontwikkelaars Hallo.

Hallo laatste werkstroom zijn als volgt:

1. Ontwikkelaars klikt op Hallo aanmelden of registreren op koppeling Hallo API Management-portal voor ontwikkelaars
2. Browser wordt omgeleid toohello delegering eindpunt
3. Eindpunt van de overdracht in leidt tooor geeft UI gevraagd gebruiker toosign in- of registreren
4. Indien geslaagd kunt is Hallo gebruiker omgeleide back toohello API Management developer portal-pagina die ze vanuit gestart

toobegin, gaan we eerste tooroute voor configuratie-API Management-aanvragen via uw eindpunt overdracht. Hallo publicatieportal van API Management, klik op **beveiliging** en klik vervolgens op Hallo **delegering** tabblad. Klik op Hallo selectievakje tooenable gemachtigde aanmelden en registreren.

![Overdracht pagina][api-management-delegation-signin-up]

* Bepaal wat Hallo-URL van uw eindpunt speciale delegering wordt en invoeren in Hallo **delegering eindpunt-URL** veld. 
* Binnen Hallo **delegering verificatiesleutel** veld Voer een geheim dat is gebruikt toocompute een tooyou opgegeven handtekening voor de verificatie-tooensure die aanvraag Hallo inderdaad afkomstig is van Azure API Management. U kunt klikken op Hallo **genereren** knop toohave API een willekeurig genereren van een sleutel voor u.

Nu u toocreate hello moet **delegering eindpunt**. Tooperform heeft een aantal acties:

1. Een aanvraag ontvangt in Hallo formulier te volgen:
   
   > *http://www.yourwebsite.com/apimdelegation?Operation=Signin&returnUrl= {URL van bronpagina} & salt = {tekenreeks} & sig = {tekenreeks}*
   > 
   > 
   
    De queryparameters voor Hallo-in- / registratie-aanvraag:
   
   * **bewerking**: welk type overdracht aanvraag is - deze kan alleen worden identificeert **SignIn** in dit geval
   * **returnUrl**: Hallo URL van Hallo pagina waar Hallo gebruiker hebt geklikt op een koppeling aanmelden of registreren
   * **Salt**: een speciale salt tekenreeks voor een hash beveiliging computing
   * **SIG**: een berekende beveiliging hash toobe gebruikt voor de vergelijking tooyour eigen berekende hash
2. Controleer of dat deze Hallo-aanvraag afkomstig is van Azure API Management (optioneel, maar sterk aanbevolen voor beveiliging)
   
   * Een HMAC SHA512-hash van een tekenreeks op basis van Hallo COMPUTE **returnUrl** en **salt** queryparameters ([voorbeeldcode hieronder]):
     
     > HMAC (**salt** + '\n' + **returnUrl**)
     > 
     > 
   * Vergelijk Hallo hierboven berekende hash toohello waarde Hallo **sig** queryparameter. Als twee Hallo-hashes overeenkomen, op de volgende stap toohello verplaatst, anders dat Hallo-aanvraag wordt geweigerd.
3. Controleer of u een aanvraag voor sign-in/aanmelding-up worden ontvangen: Hallo **bewerking** queryparameter te worden ingesteld '**SignIn**'.
4. Hallo gebruiker opleveren UI toosign in- of registreren
5. Als de gebruiker Hallo aanmelding hebt u toocreate een bijbehorende account voor hen in API Management. [Maken van een gebruiker] Hello API Management REST-API. Wanneer doet, moet u instellen van Hallo gebruiker-ID toohello tooan-ID die u kunt bijhouden van of hetzelfde in uw archief van de gebruiker is.
6. Wanneer Hallo is geverifieerd:
   
   * [eenmalige aanmelding (SSO)-token van een aanvraag] via Hallo API Management REST-API
   * een returnUrl query parameter toohello SSO-URL die u hebt ontvangen van de bovenstaande Hallo API-aanroep toevoegen:
     
     > bijvoorbeeld https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url 
     > 
     > 
   * Hallo gebruiker toohello hierboven geproduceerde URL omleiden

In aanvulling toohello **SignIn** bewerking, kunt u ook uitvoeren accountbeheer door Hallo vorige stappen te volgen en met behulp van een Hallo bewerkingen te volgen.

* **ChangePassword**
* **ChangeProfile**
* **CloseAccount**

U moet doorgeven Hallo queryparameters voor accountbeheerbewerkingen te volgen.

* **bewerking**: identificeert welk type overdracht aanvraag (ChangePassword, ChangeProfile of CloseAccount)
* **userId**: Hallo gebruikers-id van Hallo account toomanage
* **Salt**: een speciale salt tekenreeks voor een hash beveiliging computing
* **SIG**: een berekende beveiliging hash toobe gebruikt voor de vergelijking tooyour eigen berekende hash

## <a name="delegate-product-subscription"></a>Product abonnement overdragen
Product abonnement delegeren werkt op dezelfde manier toodelegating gebruiker aanmelden /-up. laatste werkstroom Hallo zou als volgt zijn:

1. Ontwikkelaar selecteert een product in Hallo API Management-portal voor ontwikkelaars en klikt op Hallo abonneren knop
2. Browser wordt omgeleid toohello delegering eindpunt
3. Overdracht eindpunt vereist product abonnement stappen worden uitgevoerd - dit is tooyou en kan leiden tot omleiding tooanother pagina toorequest factureringsgegevens, extra vragen, of het opslaan van informatie Hallo en niet een gebruikersactie vereist

tooenable hello functionaliteit op Hallo **delegering** pagina op **delegeren product abonnement**.

Verzeker u ervan Hallo delegering eindpunt voert Hallo van de volgende activiteiten:

1. Een aanvraag ontvangt in Hallo formulier te volgen:
   
   > *{bewerking} http://www.yourwebsite.com/apimdelegation?Operation= & productId = {product toosubscribe naar} & userId = {user aanvraag} & salt = {tekenreeks} & sig = {tekenreeks}*
   > 
   > 
   
    De queryparameters voor Hallo product abonnement geval:
   
   * **bewerking**: identificeert welk type overdracht aanvraag is. Voor het product abonnement zijn aanvragen Hallo geldige opties:
     * 'Abonneren': een verzoek toosubscribe Hallo gebruiker tooa opgegeven product met opgegeven ID (Zie hieronder)
     * 'Afmelden': een verzoek toounsubscribe een gebruiker vanuit een product
     * 'Vernieuwen': een verzoek toorenew een abonnement (bijvoorbeeld die kan verlopen)
   * **productId**: Hallo-ID van Hallo product Hallo gebruiker toosubscribe naar aangevraagd
   * **userId**: Hallo-ID van Hallo gebruiker voor wie Hallo-aanvraag wordt gedaan
   * **Salt**: een speciale salt tekenreeks voor een hash beveiliging computing
   * **SIG**: een berekende beveiliging hash toobe gebruikt voor de vergelijking tooyour eigen berekende hash
2. Controleer of dat deze Hallo-aanvraag afkomstig is van Azure API Management (optioneel, maar sterk aanbevolen voor beveiliging)
   
   * Een HMAC-SHA512 van een tekenreeks op basis van Hallo COMPUTE **productId**, **userId** en **salt** queryparameters:
     
     > HMAC (**salt** + '\n' + **productId** + '\n' + **userId**)
     > 
     > 
   * Vergelijk Hallo hierboven berekende hash toohello waarde Hallo **sig** queryparameter. Als twee Hallo-hashes overeenkomen, op de volgende stap toohello verplaatst, anders dat Hallo-aanvraag wordt geweigerd.
3. De verwerking van een abonnement die op basis van Hallo type in de aangevraagde bewerking uitvoeren **bewerking** -bijvoorbeeld facturering, meer vragen, enzovoort.
4. Abonneren op het met succes abonneren Hallo gebruiker toohello product op uw kant, Hallo gebruiker toohello API Management-product door [aanroepen Hallo REST-API voor het product abonnement].

## <a name="delegate-example-code"></a> Voorbeeldcode
Deze voorbeelden tonen hoe code tootake hello *delegering validatiesleutel*, die is ingesteld in overdracht welkomstscherm van de publicatieportal hello, toocreate een HMAC die vervolgens toovalidate Hallo handtekening, aan te tonen Hallo geldigheid van Hallo gebruikt doorgegeven returnUrl. Hallo dezelfde code voor Hallo productId en userId met kleine wijziging werkt.

**C#-code toogenerate hash van returnUrl**

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

**NodeJS code toogenerate hash van returnUrl**

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

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over delegering Hallo video te volgen.

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

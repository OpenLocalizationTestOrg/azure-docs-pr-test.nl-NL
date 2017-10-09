### <a name="server-auth"></a>Procedure: Verifiëren bij een provider (Server Flow)
toohave Mobile Apps beheren Hallo verificatieproces in uw app, moet u uw app registreren met de id-provider. In Azure App Service moet u tooconfigure Hallo toepassings-ID en geheim geleverd door uw provider.
Zie voor meer informatie, Hallo zelfstudie [toevoegen verificatie tooyour app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).

Wanneer u de id-provider hebt geregistreerd, aanroepen Hallo `.login()` methode met de naam van uw provider Hallo. Bijvoorbeeld: toologin met Facebook Hallo volgende code gebruiken:

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

geldige waarden voor de provider Hallo Hallo zijn 'aad', 'facebook', 'google', 'microsoftaccount' en 'twitter'.

> [!NOTE]
> Verificatie via Google werkt momenteel niet via Server Flow.  tooauthenticate met Google, moet u een [client-flow-methode](#client-auth).

In dit geval beheert Azure App Service Hallo OAuth 2.0-verificatiestroom.  Het Hallo-aanmeldingspagina van de geselecteerde provider hello wordt weergegeven en genereert een App Service-verificatietoken na geslaagde aanmelding met Hallo id-provider. Hallo aanmelding functie, retourneert als u klaar een JSON-object dat toegang biedt tot zowel de Hallo gebruikers-ID en de App Service-verificatietoken in Hallo userId authenticationToken velden en respectievelijk. Dit token kan worden opgeslagen in de cache en opnieuw worden gebruikt totdat het verloopt.

###<a name="client-auth"></a>Procedure: Verifiëren bij een provider (Client Flow)

Uw app kan ook afzonderlijk Neem contact op met de identiteitsprovider Hallo en geef vervolgens Hallo geretourneerd token tooyour App Service voor verificatie. Deze stroom client kunt u een één-aanmeldingservaring aanpast voor gebruikers of tooretrieve extra gebruikersgegevens van de identiteitsprovider Hallo tooprovide.

#### <a name="social-authentication-basic-example"></a>Eenvoudig voorbeeld van sociale verificatie

In dit voorbeeld wordt de client-SDK van Facebook gebruikt voor verificatie:

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
In dit voorbeeld wordt ervan uitgegaan dat Hallo-token opgegeven door de respectieve provider Hallo SDK wordt opgeslagen in token Hallo-variabele.

#### <a name="microsoft-account-example"></a>Voorbeeld van Microsoft-account

Hallo wordt na Hallo Live SDK, die ondersteuning biedt voor één aanmelding voor Windows Store-apps met behulp van Microsoft-Account:

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

In dit voorbeeld krijgt een token van Live verbinding maken, die is opgegeven tooyour App Service door het Hallo-aanmelding functie aanroepen.

###<a name="auth-getinfo"></a>Hoe: ophalen van informatie over Hallo geverifieerde gebruiker

Hallo verificatie-informatie kan worden opgehaald uit Hallo `/.auth/me` -eindpunt met een HTTP-aanroepen met eventuele AJAX-bibliotheek.  Zorg ervoor dat u Hallo ingesteld `X-ZUMO-AUTH` header tooyour verificatietoken.  Hallo-verificatietoken opgeslagen in `client.currentUser.mobileServiceAuthenticationToken`.  Bijvoorbeeld: toouse Hallo ophalen API:

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // hello user object contains hello claims for hello authenticated user
    });
```

Ophalen is beschikbaar als [npm-pakket](https://www.npmjs.com/package/whatwg-fetch), maar kan ook met een browser worden gedownload van [CDNJS](https://cdnjs.com/libraries/fetch). U kunt ook jQuery of een andere AJAX-API toofetch Hallo-informatie.  Gegevens worden ontvangen als JSON-object.

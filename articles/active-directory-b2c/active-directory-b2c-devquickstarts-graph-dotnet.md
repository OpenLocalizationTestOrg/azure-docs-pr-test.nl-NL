---
title: 'Azure Active Directory B2C: Gebruik Hallo Graph API | Microsoft Docs'
description: Hoe Hallo toocall Graph API voor een B2C-tenant met behulp van een toepassing identiteit tooautomate Hallo-proces.
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a>Azure AD B2C: Hallo Graph API gebruiken
Azure Active Directory (Azure AD) B2C tenants vaak zeer grote toobe. Dit betekent dat veel algemene beheertaken voor tenant toobe via een programma wordt uitgevoerd moeten. Een voorbeeld van een primaire is Gebruikersbeheer. Mogelijk moet u een bestaande gebruiker store tooa B2C-tenant toomigrate. U kunt toohost gebruikersregistratie wilt op de pagina en gebruikersaccounts maken in uw Azure AD B2C-directory achter de schermen Hallo. Deze typen taken vereist Hallo mogelijkheid toocreate, lezen, bijwerken en verwijderen van gebruikersaccounts. U kunt deze taken uitvoeren met behulp van hello Azure AD Graph API.

Voor B2C-tenants zijn er twee primaire modi voor de communicatie met de Hallo Graph API.

* Voor interactieve, eenmalige taken, moet u fungeren als een administrator-account in Hallo B2C-tenant wanneer u Hallo taken uitvoeren. In deze modus moet een beheerder toosign met referenties waarover de beheerder om een toohello aanroepen Graph API kan uitvoeren.
* Voor de geautomatiseerde, continue taken, moet u een type van service-account dat u opgeeft met Hallo benodigde bevoegdheden tooperform beheertaken. In Azure AD kunt u dit doen door een toepassing registreren en tooAzure AD verifiëren. Dit wordt gedaan met behulp van een **toepassings-ID** die gebruikmaakt van Hallo [OAuth 2.0-clientreferenties verlenen](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api). In dit geval fungeert Hallo toepassing als zichzelf niet als een gebruiker toocall Hallo Graph API.

In dit artikel bespreken we hoe tooperform Hallo geautomatiseerde gebruiksvoorbeeld. toodemonstrate, gaan we gaat verder met een .NET 4.5 `B2CGraphClient` die de gebruiker voert maken, lezen, bijwerken en verwijderen (CRUD)-bewerkingen. Hallo-client heeft een Windows-opdrachtregelinterface (CLI) waarmee u tooinvoke verschillende methoden. Hallo-code is echter toobehave geschreven in een niet-interactieve, geautomatiseerde manier.

## <a name="get-an-azure-ad-b2c-tenant"></a>Een Azure AD B2C-tenant verkrijgen
Voordat u kunt maken van toepassingen of gebruikers of helemaal met Azure AD communiceren, moet u een Azure AD B2C-tenant en een globale beheerdersaccount in Hallo-tenant. Als u nog geen een tenant hebt, [aan de slag met Azure AD B2C](active-directory-b2c-get-started.md).

## <a name="register-your-application-in-your-tenant"></a>Uw toepassing registreren in uw tenant
Nadat u een B2C-tenant hebt, moet u tooregister uw toepassing via Hallo [Azure Portal](https://portal.azure.com).

> [!IMPORTANT]
> toouse hello Graph API met uw B2C-tenant, moet u een specifieke toepassing tooregister met behulp van algemene Hallo *App registraties* blade in Azure Portal Hallo **niet** Azure AD B2C  *Toepassingen* blade. U niet opnieuw gebruiken Hallo reeds bestaande B2C toepassingen die u hebt geregistreerd in Azure AD B2C Hallo *toepassingen* blade.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Uw account selecteren in Hallo rechtsboven Hallo pagina kiest u uw Azure AD B2C-tenant.
3. In Hallo links navigatiedeelvenster kiest **meer Services**, klikt u op **App registraties**, en klik op **toevoegen**.
4. Volg de aanwijzingen Hallo en maak een nieuwe toepassing. 
    1. Selecteer **Web-App / API** zoals Hallo toepassingstype.    
    2. Geef **een omleidings-URI** (bijvoorbeeld https://B2CGraphAPI) als het is niet relevant zijn voor dit voorbeeld.  
5. Hallo toepassing wordt nu weergegeven in de lijst Hallo van toepassingen, klikt u op de tooobtain hello **toepassings-ID** (ook wel bekend als een Client-ID). Kopieer de verbindingsreeks als u hebt deze nodig in een volgende sectie.
6. Klik op de blade instellingen hello, op **sleutels** en voeg een nieuwe sleutel (ook wel bekend als clientgeheim). Ook het kopiëren voor gebruik in een volgende sectie.

## <a name="configure-create-read-and-update-permissions-for-your-application"></a>Configureer maken, lezen en bijwerken van machtigingen voor uw toepassing
Nu u tooconfigure moet uw toepassing tooget die alle Hallo machtigingen toocreate vereist, lezen, bijwerken en verwijderen van gebruikers.

1. Als u doorgaat in Azure portal App registraties blade hello, selecteer uw toepassing.
2. Klik op de blade instellingen hello, op **vereist machtigingen**.
3. Klik in de blade Hallo vereiste machtigingen op **Windows Azure Active Directory**.
4. Selecteer Hallo Hallo toegang inschakelen Blade **lezen en schrijven directorygegevens** machtiging van **Toepassingsmachtigingen** en klik op **opslaan**.
5. Ten slotte terug in de blade van de vereiste machtigingen hello, klik op Hallo **machtiging verlenen** knop.

U hebt nu een toepassing die gemachtigd toocreate, lezen en bijwerken gebruikers van uw B2C-tenant is.

## <a name="configure-delete-permissions-for-your-application"></a>Verwijdermachtigingen voor uw toepassing configureren
Op dit moment Hallo *lezen en schrijven directorygegevens* machtiging heeft **niet** Hallo mogelijkheid toodo omvatten alle verwijderingen zoals het verwijderen van gebruikers. Als u wilt dat toogive toepassing hello mogelijkheid toodelete gebruikers, moet u toodo deze extra stappen die betrekking hebben op PowerShell, anders kunt u de volgende sectie toohello overslaan.

Eerst downloaden en installeren van Hallo [Microsoft Online Services-aanmeldhulp](http://go.microsoft.com/fwlink/?LinkID=286152). Download en installeer Hallo vervolgens [64-bits Azure Active Directory-module voor Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).

Nadat u Hallo PowerShell-module geïnstalleerd, opent u PowerShell en verbinding maken met tooyour B2C-tenant. Nadat u hebt uitgevoerd `Get-Credential`, wordt u gevraagd om een gebruikersnaam en wachtwoord, Enter Hallo-gebruikersnaam en wachtwoord van uw B2C-tenant administrator-account.

> [!IMPORTANT]
> U moet toouse een B2C-tenant administrator-account dat is **lokale** toohello B2C-tenant. Deze accounts moeten uitzien: myusername@myb2ctenant.onmicrosoft.com.

```powershell
Connect-MsolService
```

Nu we hello gebruiken **toepassings-ID** in onderstaande tooassign Hallo toepassing hello account administrator gebruikersrol waarmee deze toodelete gebruikers Hallo-script. Deze rollen hebben een bekende id's, dus u hoeft alleen toodo wordt ingevoerd uw **toepassings-ID** in onderstaande Hallo-script.

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

Nu uw toepassing heeft ook machtigingen toodelete gebruikers van uw B2C-tenant.

## <a name="download-configure-and-build-hello-sample-code"></a>Downloaden, configureren en voorbeeldcode Hallo bouwen
Eerst Hallo voorbeeldcode downloaden en deze uitgevoerd. Het duurt we vervolgens een nader bekijken.  U kunt [Hallo voorbeeldcode als ZIP-bestand downloaden](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip). U kunt dit ook klonen naar een map van uw keuze:

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

Open Hallo `B2CGraphClient\B2CGraphClient.sln` Visual Studio-oplossing in Visual Studio. In Hallo `B2CGraphClient` project, open Hallo bestand `App.config`. Hallo drie app-instellingen vervangen door uw eigen waarden:

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

Vervolgens met de rechtermuisknop op Hallo `B2CGraphClient` oplossing en rebuild Hallo-voorbeeld. Als u geslaagde, u hebt nu een `B2C.exe` uitvoerbare bestand zich in `B2CGraphClient\bin\Debug`.

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a>Gebruiker CRUD-bewerkingen met behulp van Hallo Graph API bouwen
toouse hello B2CGraphClient, open een `cmd` Windows command prompt en wijzigen van uw directory toohello `Debug` directory. Voer Hallo `B2C Help` opdracht.

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

Hiermee wordt een korte beschrijving van elke opdracht weergegeven. Telkens wanneer u een van deze opdrachten aanroepen `B2CGraphClient` maakt u een aanvraag toohello Azure AD Graph API.

### <a name="get-an-access-token"></a>Een toegangstoken opvragen
Een aanvraag toohello Graph API vereist een toegangstoken voor verificatie. `B2CGraphClient`maakt gebruik van Hallo open source Active Directory Authentication Library (ADAL) toohelp toegangstokens te verkrijgen. ADAL gemakkelijker token overname door te geven van een eenvoudige API en wordt gelet op een aantal belangrijke details, zoals caching toegangstokens. U hebt geen toouse ADAL tooget tokens, hoewel. U kunt ook tokens ophalen door HTTP-aanvragen.

> [!NOTE]
> Deze voorbeeldcode maakt gebruik van ADAL v2 in volgorde toocommunicate Hello Graph API.  U moet in volgorde tooget toegangstokens die kunnen worden gebruikt met Azure AD Graph API Hallo ADAL v2 of v3 gebruiken.
> 
> 

Wanneer `B2CGraphClient` wordt uitgevoerd, maakt het een exemplaar van Hallo `B2CGraphClient` klasse. Hallo-constructor voor deze klasse stelt u een steigers ADAL-verificatie:

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

We gebruiken Hallo `B2C Get-User` opdracht als voorbeeld. Wanneer `B2C Get-User` wordt aangeroepen zonder eventuele extra ingangen, Hallo CLI aanroepen Hallo `B2CGraphClient.GetAllUsers(...)` methode. Deze methode aanroept `B2CGraphClient.SendGraphGetRequest(...)`, die een HTTP GET-aanvraag toohello Graph API worden verzonden. Voordat u `B2CGraphClient.SendGraphGetRequest(...)` verzendt Hallo GET-aanvraag, eerst krijgt een token met behulp van ADAL:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

U kunt een toegangstoken ophalen voor Hallo Graph API door aanroepen Hallo ADAL `AuthenticationContext.AcquireToken(...)` methode. ADAL retourneert een `access_token` die Hallo toepassingsidentiteit vertegenwoordigt.

### <a name="read-users"></a>Lezen van gebruikers
Als u een lijst met gebruikers tooget of een bepaalde gebruiker uit Hallo Graph API ophalen, kunt u een HTTP verzenden `GET` toohello aanvragen `/users` eindpunt. Een aanvraag voor alle gebruikers in een tenant Hallo ziet er als volgt:

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee dit verzoek uitvoeren:

 ```
 > B2C Get-User
 ```

Er zijn twee belangrijke zaken toonote:

* Hallo toegangstoken is verkregen via de ADAL wordt toegevoegd toohello `Authorization` header met behulp van Hallo `Bearer` schema.
* Voor B2C-tenants, moet u de queryparameter Hallo `api-version=1.6`.

Beide van deze gegevens worden verwerkt in de Hallo `B2CGraphClient.SendGraphGetRequest(...)` methode:

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a>Maak gebruikersaccounts van consumenten
Wanneer u gebruikersaccounts in uw B2C-tenant maken, kunt u een HTTP verzenden `POST` toohello aanvragen `/users` eindpunt:

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

De meeste van deze eigenschappen in deze aanvraag zijn vereiste toocreate consumer gebruikers. toolearn meer, klikt u op [hier](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser). Houd er rekening mee dat Hallo `//` opmerkingen zijn opgenomen ter illustratie. Neem ze niet in een werkelijke-aanvraag.

toosee hello aanvraag, voer een van de volgende opdrachten Hallo:

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

Hallo `Create-User` opdracht gebruikt u een .json-bestand als invoerparameter. Dit document bevat een JSON-weergave van een gebruikersobject. Er zijn twee voorbeeldbestanden .json in de voorbeeldcode Hallo: `usertemplate-email.json` en `usertemplate-username.json`. Uw behoeften, kunt u deze bestanden toosuit wijzigen. Bovendien toohello bovenstaande velden vereist, verschillende optionele velden die u kunt gebruiken, zijn opgenomen in deze bestanden. Meer informatie over de optionele velden Hallo vindt u in Hallo [entiteitsverwijzing Azure AD Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).

U kunt zien hoe Hallo POST-aanvraag is geconstrueerd in `B2CGraphClient.SendGraphPostRequest(...)`.

* Het toevoegen van een token toohello toegang `Authorization` koptekst van Hallo-aanvraag.
* Hiermee `api-version=1.6`.
* Hallo JSON gebruikersobject in Hallo hoofdtekst van Hallo aanvraag opgenomen.

> [!NOTE]
> Als het Hallo-computeraccounts die u wilt dat toomigrate uit een bestaande gebruiker store heeft lagere Wachtwoordsterkte dan Hallo [sterk Wachtwoordsterkte afgedwongen door Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), kunt u uitschakelen Hallo sterk wachtwoord vereist met Hallo `DisableStrongPassword`waarde in Hallo `passwordPolicies` eigenschap. Bijvoorbeeld, kunt u Hallo gebruikersaanvraag hierboven beschreven als volgt maken: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.
> 
> 

### <a name="update-consumer-user-accounts"></a>Gebruikersaccounts van consumenten bijwerken
Tijdens het bijwerken van gebruikersobjecten wordt hello vergelijkbaar toohello account dat u gebruikersobjecten toocreate gebruikt. Maar dit proces maakt gebruik van HTTP Hallo `PATCH` methode:

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

Probeer tooupdate een gebruiker door het bijwerken van uw JSON-bestanden met nieuwe gegevens. Vervolgens kunt u `B2CGraphClient` toorun een van deze opdrachten:

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

Hallo inspecteren `B2CGraphClient.SendGraphPatchRequest(...)` methode voor meer informatie over het toosend deze aanvraag.

### <a name="search-users"></a>Gebruikers zoeken
U kunt zoeken naar gebruikers in uw B2C-tenant in een aantal manieren. Een met behulp van de object-ID of twee, met behulp van de gebruiker van het Hallo-aanmelden-id van gebruiker hello (dat wil zeggen, Hallo `signInNames` eigenschap).

Voer een van de Hallo opdrachten toosearch voor een specifieke gebruiker volgen:

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

Hier volgen enkele voorbeelden:

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a>Gebruikers verwijderen
Hallo-proces voor het verwijderen van een gebruiker is eenvoudig. Gebruik Hallo HTTP `DELETE` methode en constructie Hallo-URL met Hallo corrigeren object-ID:

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

toosee bijvoorbeeld Voer deze opdracht en weergave Hallo delete-aanvraag die is afgedrukt toohello console:

```
> B2C Delete-User <object-id-of-user>
```

Hallo inspecteren `B2CGraphClient.SendGraphDeleteRequest(...)` methode voor meer informatie over het toosend deze aanvraag.

U kunt veel andere acties Hello Azure AD Graph API in toevoeging toouser beheer uitvoeren. De [Azure AD Graph API-referentiemateriaal](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) worden details weergegeven over elke actie, samen met de voorbeeld-aanvragen.

## <a name="use-custom-attributes"></a>Aangepaste kenmerken gebruiken
De meeste toepassingen van de consument moeten toostore een type aangepaste gebruikersprofielgegevens. Een manier die u kunt dit doen is toodefine een aangepast kenmerk in uw B2C-tenant. U kunt vervolgens dat kenmerk Hallo behandelen dezelfde manier als u een andere eigenschap van een gebruikersobject behandelen. U kunt bijwerken Hallo-kenmerk verwijderen Hallo kenmerk query door het Hallo-kenmerk Hallo kenmerk verzenden als claim in aanmelden tokens en meer.

een aangepast kenmerk in uw B2C-tenant, toodefine Zie Hallo [B2C aangepast kenmerkverwijzing](active-directory-b2c-reference-custom-attr.md).

U kunt bekijken Hallo aangepaste kenmerken die worden gedefinieerd in uw B2C-tenant met behulp van `B2CGraphClient`:

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

Hallo-uitvoer van deze functies blijkt Hallo details van elk aangepast kenmerk, zoals:

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

U kunt Hallo volledige naam, zoals `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, als een eigenschap van de gebruikersobjecten.  .Json-bestand bijwerken met de nieuwe eigenschap Hallo en een waarde voor eigenschap Hallo en voer vervolgens:

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

Met behulp van `B2CGraphClient`, hebt u een servicetoepassing die uw gebruikers B2C-tenant programmatisch kunt beheren. `B2CGraphClient`maakt gebruik van een eigen toepassing identiteit tooauthenticate toohello Azure AD Graph API. Ook krijgt deze tokens met behulp van een clientgeheim. Als u deze functionaliteit in uw toepassing opnemen, houd rekening met enkele belangrijke punten voor B2C-apps:

* U moet toogrant Hallo toepassing hello juiste machtigingen in Hallo-tenant.
* Nu moet u toouse ADAL (geen MSAL) tooget toegangstokens. (U kunt ook verzenden protocolberichten rechtstreeks, zonder gebruik van een bibliotheek.)
* Wanneer u Hallo Graph API aanroept, gebruik `api-version=1.6`.
* Wanneer u maken en consumenten gebruikers bij te werken, is enkele eigenschappen zijn vereist, zoals hierboven is beschreven.

Als u vragen of aanvragen voor acties die u tooperform wilt via Hallo Graph API op uw B2C-tenant, een opmerking voor dit artikel laat bestanden of een probleem in Hallo GitHub code voorbeeld-opslagplaats.


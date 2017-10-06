---
title: aaaAzure Active Directory-verificatie en Resource Manager | Microsoft Docs
description: Een ontwikkelaar handleiding tooauthentication met hello Azure Resource Manager-API en Azure Active Directory voor het integreren van een app met andere Azure-abonnementen.
services: azure-resource-manager,active-directory
documentationcenter: na
author: dushyantgill
manager: timlt
editor: tysonn
ms.assetid: 17b2b40d-bf42-4c7d-9a88-9938409c5088
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/27/2016
ms.author: dugill;tomfitz
ms.openlocfilehash: 757e45fdb28488b45de70647746461888bf35a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-resource-manager-authentication-api-tooaccess-subscriptions"></a>Gebruik resourcemanager authenticatie-API tooaccess abonnementen
## <a name="introduction"></a>Inleiding
Als u een softwareontwikkelaar die moet toocreate een app die van de klant Azure-resources wordt beheerd, dit onderwerp leest u hoe tooauthenticate met hello Azure Resource Manager-API's en tooresources in andere abonnementen toegang te krijgen.

Uw app hebben toegang tot Hallo Resource Manager-API's in verschillende manieren:

1. **Gebruikers- + toegang tot Apps**: voor apps die toegang krijgen bronnen namens een gebruiker aangemeld tot. Deze methode werkt voor apps, zoals web-apps en opdrachtregelprogramma's, die betrekking op alleen 'interactieve management' Azure-resources hebben.
2. **App-lezentoegang**: voor apps die daemon-services en geplande taken worden uitgevoerd. Hallo-app identiteit krijgt directe toegang tot toohello bronnen. Deze methode werkt voor apps die langlopende headless (zonder toezicht) toegang tooAzure nodig.

Dit onderwerp vindt u stapsgewijze instructies toocreate een app die gebruikmaakt van deze twee autorisatiemethoden. Er wordt weergegeven hoe tooperform elke stap met REST-API of C#. de volledige ASP.NET MVC-toepassing Hello is beschikbaar op [https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense](https://github.com/dushyantgill/VipSwapper/tree/master/CloudSense).

## <a name="what-hello-web-app-does"></a>Welke Hallo web-app biedt
Hallo-web-app:

1. Zich aanmeldt een Azure-gebruiker.
2. Gebruiker toogrant Hallo web app toegang tooResource Manager vraagt.
3. Gebruikers- + toegangstoken app opgehaald voor toegang tot de Resource Manager.
4. Gebruikt (uit stap 3) token toocall Resource Manager en de functie toewijzen Hallo app service-principal tooa in Hallo-abonnement waarmee Hallo app op lange termijn toegang toohello abonnement.
5. App-lezentoegang token opgehaald.
6. Token (uit stap 5) toomanage bronnen worden gebruikt in het Hallo-abonnement via Resource Manager.

Hier volgt Hallo end-to-end-stroom van Hallo-webtoepassing.

![Resource Manager-authenticatiestroom](./media/resource-manager-api-authentication/Auth-Swim-Lane.png)

Als een gebruiker u Hallo abonnements-id opgeven voor Hallo abonnement u wilt dat toouse:

![abonnement-id opgeven](./media/resource-manager-api-authentication/sample-ux-1.png)

Selecteer Hallo account toouse voor logboekregistratie in.

![account selecteren](./media/resource-manager-api-authentication/sample-ux-2.png)

Geef uw referenties.

![referenties opgeven](./media/resource-manager-api-authentication/sample-ux-3.png)

Hallo app toegang tooyour Azure-abonnementen verlenen:

![Toegang verlenen](./media/resource-manager-api-authentication/sample-ux-4.png)

Uw verbonden abonnementen beheren:

![Verbinding maken met abonnement](./media/resource-manager-api-authentication/sample-ux-7.png)

## <a name="register-application"></a>Toepassing registreren
Voordat u begint met het coderen, registreert u uw web-app met Azure Active Directory (AD). Hallo app registratie maakt een centrale identiteit voor uw app in Azure AD. Deze bevat algemene informatie over uw toepassing zoals OAuth-Clientidentiteit, antwoord-URL's en de referenties die uw toepassing tooauthenticate en toegang tot Azure Resource Manager-API's gebruikt. app-registratie Hallo registreert ook verschillende machtigingen die uw toepassing moet overgedragen bij het openen van Microsoft APIs namens de gebruiker Hallo Hallo.

Omdat uw app toegang krijgt andere abonnement tot, moet u deze configureren als een multitenant-toepassing. validatie van toopass bieden een die zijn gekoppeld aan uw Azure Active Directory-domein. toosee hello domeinen die zijn gekoppeld aan uw Azure Active Directory, aanmelden toohello [klassieke portal](https://manage.windowsazure.com). Selecteer uw Azure Active Directory en selecteer vervolgens **domeinen**.

Hallo volgende voorbeeld ziet u hoe tooregister app Hallo met behulp van Azure PowerShell. U moet Hallo meest recente versie (augustus 2016) van Azure PowerShell voor deze opdracht toowork hebben.

    $app = New-AzureRmADApplication -DisplayName "{app name}" -HomePage "https://{your domain}/{app name}" -IdentifierUris "https://{your domain}/{app name}" -Password "{your password}" -AvailableToOtherTenants $true

toolog in als Hallo AD-toepassing, moet u Hallo toepassings-id en wachtwoord. toosee hello toepassings-id die wordt geretourneerd vanaf Hallo vorige opdracht gebruiken:

    $app.ApplicationId

Hallo volgende voorbeeld ziet u hoe tooregister app Hallo met Azure CLI.

    azure ad app create --name {app name} --home-page https://{your domain}/{app name} --identifier-uris https://{your domain}/{app name} --password {your password} --available true

Hallo resultaten bevatten Hallo AppId die u bij het verifiëren van de toepassing hello moet.

### <a name="optional-configuration---certificate-credential"></a>Optionele configuratie - certificaat-referentie
Daarnaast ondersteunt Azure AD referenties van het computercertificaat voor toepassingen: maken van een zelfondertekend certificaat, blijven de persoonlijke sleutel Hallo en Hallo openbare sleutel tooyour Azure AD-toepassing registreren toevoegen. Voor verificatie verzendt uw toepassing een kleine nettolading tooAzure AD ondertekend met de persoonlijke sleutel en Azure AD valideert Hallo-handtekening met de Hallo openbare sleutel die u hebt geregistreerd.

Zie voor meer informatie over het maken van een AD-app met een certificaat [gebruik Azure PowerShell toocreate een service-principal tooaccess resources](resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) of [gebruik Azure CLI toocreate een service-principal tooaccess resources](resource-group-authenticate-service-principal-cli.md#create-service-principal-with-certificate).

## <a name="get-tenant-id-from-subscription-id"></a>Tenant-id ophalen van abonnement-id
een token dat gebruikt toocall Resource Manager worden kan toorequest, uw toepassing moet tooknow hello tenant-ID van hello Azure AD-tenant die als host fungeert voor hello Azure-abonnement. Waarschijnlijk weet dat uw gebruikers hun abonnement-id's, maar ze mogelijk niet op de hoogte van de tenant id's voor Azure Active Directory. tooget hello gebruiker Hallo van de tenant-id van gebruiker vragen voor Hallo abonnements-id. Bieden die abonnements-id bij het verzenden van een aanvraag over Hallo abonnement:

    https://management.azure.com/subscriptions/{subscription-id}?api-version=2015-01-01

Hallo-aanvraag mislukt, omdat Hallo gebruiker heeft geen nog aangemeld, maar u Hallo tenant-id uit het antwoord Hallo ophalen kunt. In deze uitzondering ophalen Hallo tenant-id Hallo antwoord header-waarde voor **WWW-verificatie**. U ziet deze implementatie in Hallo [GetDirectoryForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L20) methode.

## <a name="get-user--app-access-token"></a>Gebruikers- + app toegangstoken ophalen
Uw toepassing hello gebruiker tooAzure AD met een OAuth 2.0 autoriseren - tooauthenticate Hallo van de gebruiker referenties aanvragen worden omgeleid en ophalen van een autorisatiecode. Uw toepassing gebruikt Hallo autorisatie code tooget een toegangstoken voor Resource Manager. Hallo [ConnectSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/Controllers/HomeController.cs#L42) methode Hallo autorisatieaanvraag maakt.

Dit onderwerp leest Hallo REST-API-aanvragen tooauthenticate Hallo gebruiker. U kunt ook helper bibliotheken tooperform verificatie gebruiken in uw code. Zie voor meer informatie over deze bibliotheken [Azure Active Directory Authentication Libraries](../active-directory/active-directory-authentication-libraries.md). Zie voor instructies over het integreren van identiteitsbeheer in een toepassing [ontwikkelaarshandleiding Azure Active Directory](../active-directory/active-directory-developers-guide.md).

### <a name="auth-request-oauth-20"></a>Aanvraag voor verificatie (OAuth 2.0)
Een Open ID Connect/OAuth2.0 autoriseren aanvragen toohello Azure AD geautoriseerde eindpunt uitgeven:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize

Hallo queryreeksparameters die beschikbaar voor deze aanvraag zijn worden beschreven in Hallo [aanvragen van een autorisatiecode](../active-directory/develop/active-directory-protocols-oauth-code.md#request-an-authorization-code) onderwerp.

Hallo volgende voorbeeld wordt getoond hoe toorequest OAuth2.0 autorisatie:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=query&response_type=code&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&domain_hint=live.com

Azure AD verifieert de gebruiker Hallo en, indien nodig, vraagt Hallo gebruiker toogrant machtiging toohello app. Het resultaat Hallo autorisatie code toohello antwoord-URL van uw toepassing. Afhankelijk van Hallo aangevraagd response_mode, Azure AD beide verzendt terug Hallo gegevens in de queryreeks of als post-gegevens.

    code=AAABAAAAiL****FDMZBUwZ8eCAA&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="auth-request-open-id-connect"></a>Verificatieaanvragen (Open ID Connect)
Als u niet alleen tooaccess Azure Resource Manager namens de gebruiker hello wilt, maar ook toestaan dat Hallo gebruiker toosign tooyour toepassing hun Azure AD-account, geven u een Open ID Connect autoriseren Request. Met Open ID Connect ontvangt de toepassing ook een id_token van Azure AD die uw app in Hallo gebruiker toosign kunt gebruiken.

Hallo queryreeksparameters die beschikbaar voor deze aanvraag zijn worden beschreven in Hallo [Hallo aanmelden Verzendaanvraag](../active-directory/develop/active-directory-protocols-openid-connect-code.md#send-the-sign-in-request) onderwerp.

Er is een voorbeeld van een Open ID Connect aanvraag:

     https://login.microsoftonline.com/{tenant-id}/OAuth2/Authorize?client_id=a0448380-c346-4f9f-b897-c18733de9394&response_mode=form_post&response_type=code+id_token&redirect_uri=http%3a%2f%2fwww.vipswapper.com%2fcloudsense%2fAccount%2fSignIn&resource=https%3a%2f%2fgraph.windows.net%2f&scope=openid+profile&nonce=63567Dc4MDAw&domain_hint=live.com&state=M_12tMyKaM8

Azure AD verifieert de gebruiker Hallo en, indien nodig, vraagt Hallo gebruiker toogrant machtiging toohello app. Het resultaat Hallo autorisatie code toohello antwoord-URL van uw toepassing. Afhankelijk van Hallo aangevraagd response_mode, Azure AD beide verzendt terug Hallo gegevens in de queryreeks of als post-gegevens.

Een voorbeeld Open ID Connect reactie is:

    code=AAABAAAAiL*****I4rDWd7zXsH6WUjlkIEQxIAA&id_token=eyJ0eXAiOiJKV1Q*****T3GrzzSFxg&state=M_12tMyKaM8&session_state=2d16bbce-d5d1-443f-acdf-75f6b0ce8850

### <a name="token-request-oauth20-code-grant-flow"></a>Tokenaanvraag (OAuth2.0 Code Grant stromen)
Nu uw toepassing heeft de autorisatiecode Hallo ontvangen van Azure AD, is het tijd tooget Hallo toegangstoken voor Azure Resource Manager.  Een OAuth2.0 Code Grant Token aanvragen toohello Azure AD-tokeneindpunt boeken:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Hallo queryreeksparameters die beschikbaar voor deze aanvraag zijn worden beschreven in Hallo [autorisatiecode hello gebruiken](../active-directory/develop/active-directory-protocols-oauth-code.md#use-the-authorization-code-to-request-an-access-token) onderwerp.

Hallo volgende voorbeeld ziet u een aanvraag voor code grant token met referenties van het wachtwoord:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Als u werkt met de referenties van het computercertificaat, maak een JSON Web Token (JWT) en meld u (RSA SHA256) met behulp van de persoonlijke sleutel van uw toepassing certificaat referentie Hallo. Hallo claimtypen voor Hallo token staan in [JWT-token claims](../active-directory/develop/active-directory-protocols-oauth-code.md#jwt-token-claims). Zie voor een verwijzing naar Hallo [code Active Directory Authentication Library (.NET)](https://github.com/AzureAD/azure-activedirectory-library-for-dotnet/blob/dev/src/ADAL.PCL.Desktop/CryptographyHelper.cs) toosign Client Assertion JWT-tokens.

Zie Hallo [Open ID Connect spec](http://openid.net/specs/openid-connect-core-1_0.html#ClientAuthentication) voor meer informatie over clientverificatie.

Hallo volgende voorbeeld ziet u een aanvraag voor code grant token met referenties van het certificaat:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=authorization_code&code=AAABAAAAiL9Kn2Z*****L1nVMH3Z5ESiAA&redirect_uri=http%3A%2F%2Flocalhost%3A62080%2FAccount%2FSignIn&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbG*****Y9cYo8nEjMyA

Een voorbeeld van een antwoord voor code verlenen token:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039858","not_before":"1432035958","resource":"https://management.core.windows.net/","access_token":"eyJ0eXAiOiJKV1Q****M7Cw6JWtfY2lGc5A","refresh_token":"AAABAAAAiL9Kn2Z****55j-sjnyYgAA","scope":"user_impersonation","id_token":"eyJ0eXAiOiJKV*****-drP1J3P-HnHi9Rr46kGZnukEBH4dsg"}

#### <a name="handle-code-grant-token-response"></a>Code grant token antwoord verwerkt
Een geslaagde reactie token bevat toegangstoken hello (gebruiker + app) voor Azure Resource Manager. Deze toegang token tooaccess Resource Manager namens de gebruiker Hallo maakt gebruik van uw toepassing. Hallo-levensduur van de toegangstokens die zijn uitgegeven door Azure AD is een uur. Het lijkt onwaarschijnlijk dat de webtoepassing toegangstoken van toorenew hello (gebruiker + app moet). Als het toegangstoken voor toorenew Hallo moet, gebruikt u Hallo-vernieuwingstoken dat uw toepassing in het token antwoord Hallo ontvangt. Een OAuth2.0 Token aanvragen toohello Azure AD-tokeneindpunt boeken:

    https://login.microsoftonline.com/{tenant-id}/OAuth2/Token

Hallo toouse parameters met de aanvraag voor het vernieuwen van Hallo worden beschreven in [vernieuwen Hallo toegangstoken](../active-directory/develop/active-directory-protocols-oauth-code.md#refreshing-the-access-tokens).

Hallo volgende voorbeeld laat zien hoe toouse Hallo token vernieuwen:

    POST https://login.microsoftonline.com/7fe877e6-a150-4992-bbfe-f517e304dfa0/oauth2/token HTTP/1.1

    Content-Type: application/x-www-form-urlencoded
    Content-Length: 1012

    grant_type=refresh_token&refresh_token=AAABAAAAiL9Kn2Z****55j-sjnyYgAA&client_id=a0448380-c346-4f9f-b897-c18733de9394&client_secret=olna84E8*****goScOg%3D

Hoewel vernieuwen van tokens gebruikte tooget nieuwe toegangstokens voor Azure Resource Manager, zijn ze niet geschikt voor offline toegang door uw toepassing. Hallo vernieuwen van tokens levensduur is beperkt en vernieuwen van tokens zijn gebonden toohello gebruiker. Als gebruiker Hallo Hallo organisatie verlaat, verliest Hallo toepassing hello vernieuwingstoken toegang. Deze aanpak is niet geschikt voor toepassingen die worden gebruikt door teams toomanage Azure-resources.

## <a name="check-if-user-can-assign-access-toosubscription"></a>Controleer als gebruiker toegang toosubscription kunt toewijzen
Nu uw toepassing heeft een token tooaccess Azure Resource Manager namens Hallo-gebruiker. de volgende stap Hallo tooconnect wordt uw app toohello-abonnement. Nadat u verbinding maakt, uw app deze abonnementen kunt beheren zelfs wanneer de gebruiker Hallo niet aanwezig is (op lange termijn offline toegang).

Bel voor elke tooconnect abonnement Hallo [Resource Manager lijstmachtigingen](https://docs.microsoft.com/rest/api/authorization/permissions) API toodetermine of Hallo gebruiker management toegangsrechten voor het Hallo-abonnement heeft.

Hallo [UserCanManagerAccessForSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L44) methode Hallo ASP.NET MVC-voorbeeld-app implementeert deze aanroep.

Hallo volgende voorbeeld wordt getoond hoe toorequest van een gebruiker machtigingen voor een abonnement. 83cfe939-2402-4581-b761-4f59b0a041e4 is Hallo-id van het Hallo-abonnement.

    GET https://management.azure.com/subscriptions/83cfe939-2402-4581-b761-4f59b0a041e4/providers/microsoft.authorization/permissions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiLC***lwO1mM7Cw6JWtfY2lGc5A

Een voorbeeld van Hallo antwoord tooget gebruikersmachtigingen op abonnement is:

    HTTP/1.1 200 OK

    {"value":[{"actions":["*"],"notActions":["Microsoft.Authorization/*/Write","Microsoft.Authorization/*/Delete"]},{"actions":["*/read"],"notActions":[]}]}

Hallo machtigingen API retourneert meerdere machtigingen. Elke machtiging bestaat uit de toegestane acties (acties) en niet-toegestane acties (notactions). Als een actie aanwezig in de lijst van acties van een andere machtiging toegestaan Hallo is en niet aanwezig is in de lijst met de Hallo notactions van deze machtiging, Hallo gebruiker is toegestaan tooperform die actie. **Microsoft.Authorization/RoleAssignments/Write** is Hallo actie dat die toegang rights management verleent. Uw toepassing moet Hallo machtigingen resultaat toolook regex dezelfde waarde voor deze actie tekenreeks in Hallo acties en notactions van elke machtiging parseren.

## <a name="get-app-only-access-token"></a>App-lezentoegang-token ophalen
Nu weet u als gebruiker Hallo toegang toohello Azure-abonnement kunt toewijzen. de volgende stappen Hallo zijn:

1. De identiteit van de Hallo juiste RBAC-rol tooyour van toepassing op Hallo abonnement toewijzen.
2. Hallo toegang toewijzing controleren door een query uitvoert voor machtiging van de toepassing hello op Hallo abonnement of door het openen van Resource Manager met alleen-app-token.
3. Record Hallo verbinding in de gegevensstructuur van toepassingen 'verbonden abonnementen' - Hallo-id van het Hallo-abonnement behouden blijven.

We bekijken dichter bij de eerste stap Hallo. identiteit tooassign Hallo juiste RBAC-rol toohello van de toepassing, moet u bepalen:

* Hallo-object-id van de identiteit van uw toepassing in van de gebruiker hello Azure Active Directory
* Hallo-id van Hallo RBAC-rol die uw toepassing is op Hallo abonnement vereist

Wanneer uw aanvraag wordt geverifieerd door een gebruiker uit een Azure AD, maakt deze een service-principal-object voor uw toepassing in die Azure AD. Azure kan de RBAC-rollen toobe toegewezen principals tooservice toogrant directe toegang toocorresponding toepassingen op Azure-resources. Deze actie is precies wat we willen toodo. Query hello Azure AD Graph API toodetermine Hallo id van de service-principal Hallo van uw toepassing hello aangemelde gebruiker's Azure AD.

U hoeft alleen een toegangstoken voor Azure Resource Manager - moet u een nieuwe access token toocall hello Azure AD Graph API. Machtiging tooquery van elke toepassing in Azure AD heeft een eigen service principal-object, dus een app alleen-lezen toegangstoken voldoende is.

<a id="app-azure-ad-graph" />

### <a name="get-app-only-access-token-for-azure-ad-graph-api"></a>App-lezentoegang voor Azure AD Graph API token ophalen
tooauthenticate uw app en een token tooAzure AD Graph API, get uitgeven van een Client referentie Grant OAuth2.0 stroom tokenaanvraag tooAzure AD token-eindpunt (**https://login.microsoftonline.com/ {directory_domain_name} / OAuth2/Token**).

Hallo [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs) methode Hallo ASP.net MVC-voorbeeldtoepassing een app alleen-lezen toegang token voor het gebruik van Graph API krijgt Hallo Active Directory Authentication Library voor .NET.

Hallo queryreeksparameters die beschikbaar voor deze aanvraag zijn worden beschreven in Hallo [een Token toegang aanvragen](../active-directory/develop/active-directory-protocols-oauth-service-to-service.md#request-an-access-token) onderwerp.

Een voorbeeld van de aanvraag voor de clientreferenties verlenen token:

    POST https://login.microsoftonline.com/62e173e9-301e-423e-bcd4-29121ec1aa24/oauth2/token HTTP/1.1
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 187</pre>
    <pre>grant_type=client_credentials&client_id=a0448380-c346-4f9f-b897-c18733de9394&resource=https%3A%2F%2Fgraph.windows.net%2F &client_secret=olna8C*****Og%3D

Een voorbeeld van een antwoord voor de clientreferenties verlenen token:

    HTTP/1.1 200 OK

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1432039862","not_before":"1432035962","resource":"https://graph.windows.net/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL2dyYXBoLndpbmRv****G5gUTV-kKorR-pg"}

### <a name="get-objectid-of-application-service-principal-in-user-azure-ad"></a>Object-id van de service-principal toepassing in Azure AD-gebruiker ophalen
Nu gebruiken Hallo app alleen-lezen toegang token tooquery hello [Azure AD Graph Service-Principals](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity) API toodetermine Hallo Object-Id van de service-principal in de map Hallo Hallo-toepassing.

Hallo [GetObjectIdOfServicePrincipalInOrganization](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureADGraphAPIUtil.cs#) methode Hallo ASP.net MVC-voorbeeldtoepassing implementeert deze aanroep.

Hallo volgende voorbeeld wordt getoond hoe toorequest service-principal van een toepassing. a0448380-c346-4f9f-b897-c18733de9394 is hello client-id van de toepassing hello.

    GET https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/servicePrincipals?api-version=1.5&$filter=appId%20eq%20'a0448380-c346-4f9f-b897-c18733de9394' HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJK*****-kKorR-pg

Hallo volgende voorbeeld ziet u een antwoord toohello-aanvraag voor een toepassing service principal

    HTTP/1.1 200 OK

    {"odata.metadata":"https://graph.windows.net/62e173e9-301e-423e-bcd4-29121ec1aa24/$metadata#directoryObjects/Microsoft.DirectoryServices.ServicePrincipal","value":[{"odata.type":"Microsoft.DirectoryServices.ServicePrincipal","objectType":"ServicePrincipal","objectId":"9b5018d4-6951-42ed-8a92-f11ec283ccec","deletionTimestamp":null,"accountEnabled":true,"appDisplayName":"CloudSense","appId":"a0448380-c346-4f9f-b897-c18733de9394","appOwnerTenantId":"62e173e9-301e-423e-bcd4-29121ec1aa24","appRoleAssignmentRequired":false,"appRoles":[],"displayName":"CloudSense","errorUrl":null,"homepage":"http://www.vipswapper.com/cloudsense","keyCredentials":[],"logoutUrl":null,"oauth2Permissions":[{"adminConsentDescription":"Allow hello application tooaccess CloudSense on behalf of hello signed-in user.","adminConsentDisplayName":"Access CloudSense","id":"b7b7338e-683a-4796-b95e-60c10380de1c","isEnabled":true,"type":"User","userConsentDescription":"Allow hello application tooaccess CloudSense on your behalf.","userConsentDisplayName":"Access CloudSense","value":"user_impersonation"}],"passwordCredentials":[],"preferredTokenSigningKeyThumbprint":null,"publisherName":"vipswapper"quot;,"replyUrls":["http://www.vipswapper.com/cloudsense","http://www.vipswapper.com","http://vipswapper.com","http://vipswapper.azurewebsites.net","http://localhost:62080"],"samlMetadataUrl":null,"servicePrincipalNames":["http://www.vipswapper.com/cloudsense","a0448380-c346-4f9f-b897-c18733de9394"],"tags":["WindowsAzureActiveDirectoryIntegratedApp"]}]}

### <a name="get-azure-rbac-role-identifier"></a>Azure RBAC-rol-id ophalen
tooassign hello juiste RBAC tooyour functieservice principal, moet u bepalen Hallo-id van hello Azure RBAC-rol.

Hallo juiste RBAC-rol voor uw toepassing:

* Als uw toepassing alleen Hallo-abonnement, controleert zonder dat u wijzigingen aanbrengt, moet leesmachtigingen op Hallo-abonnement. Hallo toewijzen **lezer** rol.
* Als uw toepassing hello Azure-abonnement, entiteiten maken/wijzigen/verwijderen beheert, vereist een Hallo Inzender-rechten.
  * toomanage een bepaald type resource toewijzen Hallo Inzender resourcespecifieke rollen (Virtual Machine Contributor, Virtual Network Contributor, Storage Account Inzender, enz.)
  * toomanage elk resourcetype, toewijzen Hallo **Inzender** rol.

Hallo roltoewijzing voor uw toepassing is zichtbaar toousers, dus selecteer Hallo bevoegdheid minst vereist.

Hallo aanroepen [Resource Manager roldefinitie API](https://docs.microsoft.com/rest/api/authorization/roledefinitions) toolist alle Azure RBAC-rollen en zoek vervolgens Hallo resultaat toofind Hallo doorlopen gewenst roldefinitie met de naam.

Hallo [GetRoleId](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L246) methode Hallo ASP.net MVC-voorbeeld-app implementeert deze aanroep.

Hallo volgende voorbeeld wordt getoond hoe aanvragen tooget Azure RBAC-rol-id. 09cbd307-aa71-4aca-b346-5f253e6e3ebb is Hallo-id van het Hallo-abonnement.

    GET https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV*****fY2lGc5

Hallo reactie is in de volgende indeling Hallo:

    HTTP/1.1 200 OK

    {"value":[{"properties":{"roleName":"API Management Service Contributor","type":"BuiltInRole","description":"Lets you manage API Management services, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.ApiManagement/Services/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/312a565d-c81f-4fd8-895a-4e21e48d571c","type":"Microsoft.Authorization/roleDefinitions","name":"312a565d-c81f-4fd8-895a-4e21e48d571c"},{"properties":{"roleName":"Application Insights Component Contributor","type":"BuiltInRole","description":"Lets you manage Application Insights components, but not access toothem.","scope":"/","permissions":[{"actions":["Microsoft.Insights/components/*","Microsoft.Insights/webtests/*","Microsoft.Authorization/*/read","Microsoft.Resources/subscriptions/resources/read","Microsoft.Resources/subscriptions/resourceGroups/read","Microsoft.Resources/subscriptions/resourceGroups/resources/read","Microsoft.Resources/subscriptions/resourceGroups/deployments/*","Microsoft.Insights/alertRules/*","Microsoft.Support/*"],"notActions":[]}]},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/ae349356-3a1b-4a5e-921d-050484c6347e","type":"Microsoft.Authorization/roleDefinitions","name":"ae349356-3a1b-4a5e-921d-050484c6347e"}]}

U hoeft deze API voortdurend niet toocall. Nadat u hebt vastgesteld bekende GUID van de roldefinitie Hallo Hallo, u kunt samenstellen Hallo roldefinitie-id als:

    /subscriptions/{subscription_id}/providers/Microsoft.Authorization/roleDefinitions/{well-known-role-guid}

Hier volgen bekende GUID's Hallo van veelgebruikte ingebouwde rollen:

| Rol | GUID |
| --- | --- |
| Lezer |acdd72a7-3385-48ef-bd42-f606fba81ae7 |
| Inzender |b24988ac-6180-42a0-ab88-20f7382dd24c |
| Virtual Machine Contributor |d73bb868-a0df-4d4d-bd69-98a00b01fccb |
| Virtueel netwerk Inzender |b34d265f-36f7-4a0d-a4d4-e158ca92e90f |
| Storage-Account Inzender |86e8f5dc-a6e9-4c67-9d15-de283e8eac25 |
| Website Inzender |de139f84-1756-47ae-9be6-808fbbe84772 |
| Web Plan Inzender |2cc479cb-7b4d-49a8-b449-8c00fd0f0a4b |
| SQL Server Inzender |6d8ee4ec-f05a-4a1d-8b00-a9b17e38b437 |
| SQL DB Contributor |9b7fa17d-e63e-47b0-bb0a-15c516ac86ec |

### <a name="assign-rbac-role-tooapplication"></a>RBAC-rol tooapplication toewijzen
U hebt u alles tooassign Hallo juiste RBAC-rol tooyour service-principal met behulp van Hallo [Resource Manager roltoewijzing maken](https://docs.microsoft.com/rest/api/authorization/roleassignments) API.

Hallo [GrantRoleToServicePrincipalOnSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L170) methode Hallo ASP.net MVC-voorbeeld-app implementeert deze aanroep.

Een voorbeeld van de aanvraag tooassign RBAC-rol tooapplication:

    PUT https://management.azure.com/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/microsoft.authorization/roleassignments/4f87261d-2816-465d-8311-70a27558df4c?api-version=2015-07-01 HTTP/1.1

    Authorization: Bearer eyJ0eXAiOiJKV1QiL*****FlwO1mM7Cw6JWtfY2lGc5
    Content-Type: application/json
    Content-Length: 230

    {"properties": {"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2"}}

Hallo-aanvraag worden Hallo volgende waarden gebruikt:

| GUID | Beschrijving |
| --- | --- |
| 09cbd307-aa71-4aca-b346-5f253e6e3ebb |Hallo-id van het Hallo-abonnement |
| c3097b31-7309-4c59-b4e3-770f8406bad2 |object-id van de service-principal van de toepassing hello Hallo Hallo |
| acdd72a7-3385-48ef-bd42-f606fba81ae7 |Hallo-id van de rol Lezer Hallo |
| 4f87261d-2816-465d-8311-70a27558df4c |een nieuwe guid voor de nieuwe roltoewijzing Hallo gemaakt |

Hallo reactie is in de volgende indeling Hallo:

    HTTP/1.1 201 Created

    {"properties":{"roleDefinitionId":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7","principalId":"c3097b31-7309-4c59-b4e3-770f8406bad2","scope":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb"},"id":"/subscriptions/09cbd307-aa71-4aca-b346-5f253e6e3ebb/providers/Microsoft.Authorization/roleAssignments/4f87261d-2816-465d-8311-70a27558df4c","type":"Microsoft.Authorization/roleAssignments","name":"4f87261d-2816-465d-8311-70a27558df4c"}

### <a name="get-app-only-access-token-for-azure-resource-manager"></a>App-lezentoegang-token ophalen voor Azure Resource Manager
toovalidate die app Hallo gewenst toegang op Hallo abonnement heeft, voert u een test-taak op Hallo-abonnement met een alleen-app-token.

een app alleen-lezen toegangstoken tooget Volg de instructies van sectie [alleen app-token ophalen voor Azure AD Graph API](#app-azure-ad-graph), met een andere waarde voor Hallo resourceparameter:

    https://management.core.windows.net/

Hallo [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) methode Hallo ASP.NET MVC-voorbeeldtoepassing een app alleen-lezen toegang token voor het gebruik van Azure Resource Manager krijgt Hallo Active Directory Authentication Library voor .net.

#### <a name="get-applications-permissions-on-subscription"></a>Machtigingen van de van toepassing op abonnement ophalen
toocheck die uw toepassing heeft Hallo gewenst toegang op een Azure-abonnement, wordt u mogelijk ook aanroepen Hallo [Resource Manager machtigingen](https://docs.microsoft.com/rest/api/authorization/permissions) API. Deze aanpak is vergelijkbaar toohow u vastgesteld of Hallo gebruiker Access Management-rechten voor het Hallo-abonnement heeft. Deze tijd aanroepen echter Hallo machtigingen API met Hallo app alleen-lezen toegangstoken dat u in de vorige stap Hallo ontvangen.

Hallo [ServicePrincipalHasReadAccessToSubscription](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L110) methode Hallo ASP.NET MVC-voorbeeld-app implementeert deze aanroep.

## <a name="manage-connected-subscriptions"></a>Verbonden abonnementen beheren
Wanneer Hallo juiste RBAC-rol wordt toegewezen van de toepassing tooyour service-principal op Hallo abonnement, kunt uw toepassing houden bewaking/beheren met behulp van alleen-app toegangstokens voor Azure Resource Manager.

Is niet meer kunnen tooaccess dat abonnement als eigenaar van een abonnement van uw toepassing roltoewijzing met behulp van de klassieke portal Hallo of opdrachtregelprogramma's, uw toepassing worden verwijderd. U moet in dat geval Hallo gebruiker waarschuwen dat Hallo verbinding met de Hallo abonnement vanuit externe Hallo toepassing werd verbroken en geef ze een optie te "repareren" hello verbinding. 'Herstellen' maakt hello roltoewijzing is die offline is verwijderd gewoon opnieuw.

Net zoals u Hallo tooconnect abonnementen tooyour Gebruikerstoepassing ingeschakeld, moet u Hallo gebruiker toodisconnect abonnementen te geven. Verbinding verbreken betekent Hallo roltoewijzing met service-principal van de toepassing hello op Hallo abonnement verwijderen uit een access management-oogpunt. Desgewenst kan geen status in de toepassing hello voor Hallo abonnement te worden verwijderd.
Alleen gebruikers met toegangsmachtigingen voor beheer op Hallo abonnement zijn kunnen toodisconnect Hallo abonnement.

Hallo [RevokeRoleFromServicePrincipalOnSubscription methode](https://github.com/dushyantgill/VipSwapper/blob/master/CloudSense/CloudSense/AzureResourceManagerUtil.cs#L200) Hallo ASP.net MVC-voorbeeld-app implementeert deze aanroep.

Dat is alles - gebruikers kunnen nu eenvoudig verbinding maken en beheren hun Azure-abonnementen met uw toepassing.

---
title: een Web-API-back-end met Azure Active Directory en API Management aaaProtect | Microsoft Docs
description: Meer informatie over hoe tooprotect een Web-API-back-end met Azure Active Directory en API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a>Hoe tooprotect een Web-API-back-end met Azure Active Directory en API Management
Hallo volgende video toont hoe toobuild een Web-API-back-end en beveiligen met behulp van OAuth 2.0-protocol met Azure Active Directory en API Management.  In dit artikel biedt een overzicht en aanvullende informatie voor Hallo stappen in Hallo video. Deze 24 minuut video ziet u hoe aan:

* Een Web-API-back-end bouwen en beveilig deze met AAD - begint bij 1:30
* Hallo-API in API Management - 7:10 vanaf importeren
* Hallo Developer portal toocall Hallo API - vanaf 9:09 configureren
* Een bureaubladtoepassing toocall Hallo API - vanaf 18:08 configureren
* Configureren van een JWT validatie beleid toopre-aanvragen - vanaf 20:47 autoriseren

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a>Een Azure AD-directory maken
toosecure uw Web-API-back met Azure Active Directory moet u eerst hebben een AAD-tenant. In deze video met de naam van een tenant **APIMDemo** wordt gebruikt. toocreate een AAD-tenant aanmelden toohello [klassieke Azure-Portal](https://manage.windowsazure.com) en klik op **nieuw**->**App Services**->**Active Directory**->**Directory**->**aangepast maken**. 

![Azure Active Directory][api-management-create-aad-menu]

In dit voorbeeld van een map met de naam **APIMDemo** wordt gemaakt met een standaarddomein met de naam **DemoAPIM.onmicrosoft.com**. Deze map wordt gebruikt in de gehele Hallo video.

![Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a>Een Web-API-service worden beveiligd door Azure Active Directory maken
In deze stap wordt een Web-API-back-end gemaakt met behulp van Visual Studio 2013. In deze stap van de video Hallo begint bij 1:30. toocreate Web API-back-end-project in Visual Studio klikt u op **bestand**->**nieuw**->**Project**, en kies **ASP.NET-webtoepassing Toepassing** van Hallo **Web** lijst met sjablonen. In deze video Hallo project de naam **APIMAADDemo**. Klik op **OK** toocreate Hallo project. 

![Visual Studio][api-management-new-web-app]

Klik op **Web API** van Hallo **selecteert u een lijst met sjablonen** toocreate een Web API-project. Azure Directory Authentication tooconfigure klikt u op **verificatie wijzigen**.

![Nieuw project][api-management-new-project]

Klik op **Organisatieaccounts**, en geef Hallo **domein** van uw AAD-tenant. In dit voorbeeld Hallo domein is **DemoAPIM.onmicrosoft.com**. Hallo domein van uw directory kan worden verkregen van Hallo **domeinen** tabblad van uw directory.

![Domeinen][api-management-aad-domains]

Hallo gewenst instellingen configureren in Hallo **verificatie wijzigen** dialoogvenster en klik op **OK**.

![Verificatie wijzigen][api-management-change-authentication]

Wanneer u klikt op **OK** Visual Studio probeert tooregister uw toepassing met uw Azure AD-directory en hebt u mogelijk na vragen aan gebruiker toosign in door Visual Studio. Meld u aan met een Administrator-account voor uw directory.

![Meld u aan tooVisual Studio][api-management-sign-in-vidual-studio]

tooconfigure dit project als een Azure-Web-API selectievakje Hallo vak voor **hosten in de cloud Hallo** en klik vervolgens op **OK**.

![Nieuw project][api-management-new-project-cloud]

Hebt u mogelijk na vragen aan gebruiker toosign in tooAzure en vervolgens kunt u Hallo Web-App configureren.

![Configureren][api-management-configure-web-app]

In dit voorbeeld is een nieuwe **App Service-abonnement** met de naam **APIMAADDemo** is opgegeven.

Klik op **OK** tooconfigure Hallo Web-App en Hallo-project maken.

## <a name="add-hello-code-toohello-web-api-project"></a>Hallo code toohello Web API-project toevoegen
de volgende stap Hallo in Hallo video wordt toegevoegd Hallo code toohello Web API-project. Deze stap 4:35 wordt gestart.

Hallo-Web-API in dit voorbeeld implementeert een basisrekenmachine-service met behulp van een model en een domeincontroller. tooadd hello model voor Hallo-service met de rechtermuisknop op **modellen** in **Solution Explorer** en kies **toevoegen**, **klasse**. Naam Hallo klasse `CalcInput` en klik op **toevoegen**.

Voeg de volgende Hallo `using` instructie toohello bovenaan Hallo `CalcInput.cs` bestand.

```c#
using Newtonsoft.Json;
```

Hallo gegenereerd klasse vervangen door Hallo code te volgen.

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

Met de rechtermuisknop op **domeincontrollers** in **Solution Explorer** en kies **toevoegen**->**Controller**. Kies **Web API 2-Controller - leeg** en klik op **toevoegen**. Type **CalcController** voor Hallo Controller naam en klik op **toevoegen**.

![Controller toevoegen][api-management-add-controller]

Voeg de volgende Hallo `using` instructie toohello bovenaan Hallo `CalcController.cs` bestand.

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

Hallo gegenereerd controllerklasse vervangen door Hallo code te volgen. Deze code implementeert Hallo `Add`, `Subtract`, `Multiply`, en `Divide` operations Hallo basisrekenmachine-API.

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

Druk op **F6** toobuild en controleer of Hallo-oplossing.

## <a name="publish-hello-project-tooazure"></a>Hallo project tooAzure publiceren
In deze stap Hallo Visual Studio is-project gepubliceerde tooAzure. In deze stap van de video Hallo begint bij 5:45.

toopublish Hallo project tooAzure, met de rechtermuisknop op Hallo **APIMAADDemo** in Visual Studio-project en kies **publiceren**. Hallo-standaardinstellingen behouden in Hallo **webpublicatie** dialoogvenster en klik op **publiceren**.

![Web publiceren][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a>Machtigingen toekennen toohello Azure AD-back-end-servicetoepassing
Een nieuwe aanvraag om de back-endservice hello wordt gemaakt in uw Azure AD-directory als onderdeel van het Hallo configureren en publicatieproces van uw Web-API-project. In deze stap van de video hello, worden beginnend bij 6:13 machtigingen verleend toohello Web API-back-end.

![Toepassing][api-management-aad-backend-app]

Klik op de naam Hallo Hallo toepassing tooconfigure Hallo vereist machtigingen. Navigeer toohello **configureren** tabblad en schuif omlaag toohello **machtigingen tooother toepassingen** sectie. Klik op Hallo **Toepassingsmachtigingen** -omlaag naast **Windows** **Azure Active Directory**, Hallo selectievakje voor **mapgegevenslezen**, en klik op **opslaan**.

![Machtigingen toevoegen][api-management-aad-add-permissions]

> [!NOTE]
> Als **Windows** **Azure Active Directory** is niet wordt vermeld onder machtigingen tooother toepassingen, klikt u op **toepassing toevoegen** en toe te voegen in de lijst Hallo.
> 
> 

Maak een notitie van Hallo **App Id URI** voor gebruik in een latere stap wanneer een Azure AD-toepassing is geconfigureerd voor Hallo API Management-portal voor ontwikkelaars.

![App Id URI][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a>Hallo-Web-API importeren in API Management
API's zijn geconfigureerd met Hallo API-publicatieportal, die wordt geopend via hello Azure-Portal. tooreach, klikt u op **publicatieportal** van Hallo werkbalk van uw API Management-service. Als u nog geen exemplaar van API Management-service hebt gemaakt, raadpleegt u [API Management service-exemplaar maken] [ Create an API Management service instance] in Hallo [uw eerste API beheren] [ Manage your first API] zelfstudie.

![Publicatieportal][api-management-management-console]

Bewerkingen kunnen worden [tooAPIs handmatig toegevoegd](api-management-howto-add-operations.md), of ze kunnen worden geïmporteerd. In deze video worden bewerkingen in Swagger-indeling vanaf 6:40 geïmporteerd.

Maak een bestand met de naam `calcapi.json` met de volgende inhoud en sla het tooyour computer. Zorg ervoor dat Hallo `host` kenmerk verwijst tooyour Web API-back-end. In dit voorbeeld `"host": "apimaaddemo.azurewebsites.net"` wordt gebruikt.

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

tooimport hello Rekenmachine-API, klikt u op **API's** van Hallo **API Management** menu op Hallo links en klik vervolgens op **Import API**.

![Knop API importeren][api-management-import-api]

Volgende stappen tooconfigure hello basisrekenmachine-API Hallo uitvoeren.

1. Klik op **uit bestand**, bladeren toohello `calculator.json` bestand dat u opgeslagen en klik op Hallo **Swagger** keuzerondje.
2. Type **calc** in Hallo **achtervoegsel URL Web-API** textbox.
3. Klik in het Hallo **producten (optioneel)** vak en kies **Starter**.
4. Klik op **opslaan** tooimport Hallo API.

![Nieuwe API toevoegen][api-management-import-new-api]

Zodra het Hallo-API is geïmporteerd, wordt hello overzichtspagina voor Hallo API weergegeven in de publicatieportal Hallo.

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a>Succes Hallo-API aanroepen vanuit de ontwikkelaarsportal Hallo
Op dit moment Hallo API is geïmporteerd in API Management, maar kan nog worden aangeroepen met succes vanuit de ontwikkelaarsportal Hallo omdat Hallo back-endservice is beveiligd met Azure AD-verificatie. Dit wordt geïllustreerd in Hallo video vanaf 7:40 met Hallo stappen te volgen.

Klik op **ontwikkelaarsportal** van Hallo rechtsboven kant van de publicatieportal Hallo.

![ontwikkelaarsportal][api-management-developer-portal-menu]

Klik op **API's** en klik op Hallo **Rekenmachine** API.

![ontwikkelaarsportal][api-management-dev-portal-apis]

Klik op **Try it**.

![Probeer het nu][api-management-dev-portal-try-it]

Klik op **verzenden** en noteer de antwoordstatus Hallo van **401 niet geautoriseerd**.

![Verzenden][api-management-dev-portal-send-401]

Hallo-aanvraag is niet geautoriseerd omdat Hallo-end-API is beveiligd door Azure Active Directory. Hallo-portal voor ontwikkelaars moet geconfigureerde tooauthorize ontwikkelaars met behulp van OAuth 2.0, voordat het Hallo-API op correcte wijze aanroept. Dit proces wordt beschreven in Hallo uit te voeren.

## <a name="register-hello-developer-portal-as-an-aad-application"></a>Hallo-portal voor ontwikkelaars registreren als een AAD-toepassing
eerste stap bij het configureren van Hallo developer portal tooauthorize ontwikkelaars met behulp van OAuth 2.0 Hallo is tooregister Hallo developer-portal als een AAD-toepassing. Dit wordt geïllustreerd vanaf 8:27 in Hallo video.

Navigeer toohello Azure AD-tenant van de eerste stap Hallo van deze video in dit voorbeeld **APIMDemo** en navigeer toohello **toepassingen** tabblad.

![nieuwe toepassing][api-management-aad-new-application-devportal]

Klik op Hallo **toevoegen** knop toocreate een nieuwe Azure Active Directory-toepassing, en kies **mijn organisatie ontwikkelt toepassing toevoegen**.

![nieuwe toepassing][api-management-new-aad-application-menu]

Kies **Web-toepassing en/of Web-API**, voer een naam in en klik op volgende pijl Hallo. In dit voorbeeld **APIMDeveloperPortal** wordt gebruikt.

![nieuwe toepassing][api-management-aad-new-application-devportal-1]

Voor **aanmeldings-URL** Voer Hallo-URL van uw API Management-service en toevoeg- `/signin`. In dit voorbeeld `https://contoso5.portal.azure-api.net/signin` wordt gebruikt.

Voor **App-Id-URL** Voer Hallo-URL van uw API Management-service en het toevoegen van enkele unieke tekens. Deze mag gewenste tekens lang zijn en in dit voorbeeld `https://contoso5.portal.azure-api.net/dp` wordt gebruikt. Wanneer Hallo gewenst **App-eigenschappen** zijn geconfigureerd, klikt u op Hallo vinkje toocreate Hallo toepassing.

![nieuwe toepassing][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a>Een API Management OAuth 2.0-autorisatie-server configureren
de volgende stap Hallo is tooconfigure een OAuth 2.0-autorisatie-server in API Management. Deze stap wordt geïllustreerd in de video vanaf 9:43 Hallo.

Klik op **beveiliging** in aan de linkerkant Hallo Hallo API Management-menu, klikt u op **OAuth 2.0**, en klik vervolgens op **toevoegen autorisatie** server.

![Autorisatie-server toevoegen][api-management-add-authorization-server]

Voer een naam en een optionele beschrijving in Hallo **naam** en **beschrijving** velden. Deze velden zijn gebruikte tooidentify Hallo OAuth 2.0 autorisatie server binnen Hallo API Management service-exemplaar. In dit voorbeeld **autorisatie server demo** wordt gebruikt. Later wanneer u een OAuth 2.0-server toobe voor verificatie voor een API gebruikt opgeeft, selecteert u deze naam.

Voor Hallo **Client de registratie van URL** Voer een aanduidingswaarde van de tijdelijke zoals `http://localhost`.  Hallo **Client de registratie van URL** punten toohello pagina die door gebruikers kunnen toocreate gebruiken en hun eigen accounts configureren voor OAuth 2.0-providers die ondersteuning bieden voor gebruikersbeheer van accounts. In dit voorbeeld gebruikers niet maken en hun eigen accounts configureren zodat een tijdelijke aanduiding wordt gebruikt.

![Autorisatie-server toevoegen][api-management-add-authorization-server-1]

Geef vervolgens **autorisatie eindpunt-URL** en **Token eindpunt-URL**.

![Autorisatie-server][api-management-add-authorization-server-1a]

Deze waarden kunnen worden opgehaald uit Hallo **App eindpunten** pagina Hallo AAD-toepassing die u hebt gemaakt voor het Hallo-portal voor ontwikkelaars. tooaccess hello eindpunten Navigeer toohello **configureren** voor AAD-toepassing hello tabblad en klik op **eindpunten weergeven**.

![Toepassing][api-management-aad-devportal-application]

![Eindpunten weergeven][api-management-aad-view-endpoints]

Kopiëren Hallo **OAuth 2.0-eindpunt voor autorisatie** en plak deze in Hallo **autorisatie eindpunt-URL** textbox.

![Autorisatie-server toevoegen][api-management-add-authorization-server-2]

Kopiëren Hallo **OAuth 2.0-tokeneindpunt** en plak deze in Hallo **Token eindpunt-URL** textbox.

![Autorisatie-server toevoegen][api-management-add-authorization-server-2a]

Bovendien toopasting in token Hallo-eindpunt toevoegen voor een extra inhoudparameter met de naam **resource** en gebruiken voor Hallo waarde Hallo **App Id URI** van Hallo AAD-toepassing voor Hallo back-endservice die was gemaakt tijdens het Hallo Visual Studio-project is gepubliceerd.

![App Id URI][api-management-aad-sso-uri]

Geef vervolgens referenties Hallo-client. Dit zijn Hallo referenties voor Hallo-bron die u wilt dat tooaccess, in dit geval Hallo-portal voor ontwikkelaars.

![Clientreferenties][api-management-client-credentials]

Hallo tooget **Client-Id**, navigeer toohello **configureren** tabblad Hallo AAD-toepassing voor Hallo developer-portal en kopieer Hallo **Client-Id**.

Hallo tooget **Clientgeheim** klikt u op Hallo **Selecteer duur** vervolgkeuzelijst in Hallo **sleutels** sectie en geeft u een interval. In dit voorbeeld wordt 1 jaar gebruikt.

![Client-ID][api-management-aad-client-id]

Klik op **opslaan** toosave Hallo configuratie- en Hallo sleutel. 

> [!IMPORTANT]
> Noteer deze sleutel. Wanneer u een venster hello Azure Active Directory-configuratie hebt gesloten, kan niet opnieuw Hallo sleutel weergegeven.
> 
> 

Kopiëren Hallo sleutel toohello Klembord, switch back toohello publicatieportal, plak Hallo sleutel Hallo **Clientgeheim** tekstvak en klik op **opslaan**.

![Autorisatie-server toevoegen][api-management-add-authorization-server-3]

Direct na de clientreferenties Hallo is een code machtiging grant. Deze autorisatiecode kopiëren en switch back tooyour developer-portal Azure AD-toepassing pagina configureren en plak Hallo authorization grant in Hallo **antwoord-URL** veld en klikt u op **opslaan** opnieuw.

![Antwoord-URL][api-management-aad-reply-url]

de volgende stap Hallo is tooconfigure Hallo machtigingen voor Hallo-portal voor ontwikkelaars AAD-toepassing. Klik op **Toepassingsmachtigingen** en het selectievakje in voor Hallo **mapgegevens lezen**. Klik op **opslaan** toosave dit wijzigen en klik vervolgens op **toepassing toevoegen**.

![Machtigingen toevoegen][api-management-add-devportal-permissions]

Klik op het zoekpictogram hello, type **APIM** in Hallo beginnen met het selectievakje, selecteer **APIMAADDemo**, en klik op Hallo vinkje toosave.

![Machtigingen toevoegen][api-management-aad-add-app-permissions]

Klik op **gedelegeerde machtigingen** voor **APIMAADDemo** en het selectievakje in voor Hallo **toegang APIMAADDemo**, en klik op **opslaan**. Dit kan Hallo ontwikkelaar portaltoepassing tooaccess Hallo back-endservice.

![Machtigingen toevoegen][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a>Inschakelen van OAuth 2.0-gebruikersautorisatie voor Hallo basisrekenmachine-API
Nu dat hello OAuth 2.0-server is geconfigureerd, kunt u deze kunt opgeven in de beveiligingsinstellingen Hallo voor uw API. Deze stap wordt geïllustreerd in Hallo video vanaf 14:30.

Klik op **API's** in Hallo menu aan de linkerkant en klik op **Rekenmachine** tooview en configureer de instellingen.

![Rekenmachine-API][api-management-calc-api]

Navigeer toohello **beveiliging** tabblad, controleert u Hallo **OAuth 2.0** selectievakje, selecteer Hallo gewenste autorisatie server uit Hallo **autorisatie server** vervolgkeuzelijst en klik op **Opslaan**.

![Rekenmachine-API][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a>Alleen Hallo basisrekenmachine-API aanroepen vanuit de ontwikkelaarsportal Hallo
Nu dat Hallo OAuth 2.0-autorisatie op Hallo API is geconfigureerd, kunnen bewerkingen met succes worden aangeroepen vanuit Hallo developer center. Deze stap wordt geïllustreerd in Hallo video om 15:00 uur wordt gestart.

Navigeer terug toohello **twee gehele getallen toevoegen** bewerking van Hallo Rekenmachine service in Hallo developer-portal en klik op **Try it**. Opmerking Hallo nieuw item in Hallo **autorisatie** sectie bijbehorende toohello autorisatie server u zojuist hebt toegevoegd.

![Rekenmachine-API][api-management-calc-authorization-server]

Selecteer **autorisatiecode** van Hallo autorisatie vervolgkeuzelijst en voer de referenties op Hallo van Hallo account toouse. Als u al bent aangemeld bij Hallo-account is u mogelijk niet gevraagd.

![Rekenmachine-API][api-management-devportal-authorization-code]

Klik op **verzenden** en Opmerking Hallo **antwoordstatus** van **200 OK** en Hallo resultaten van antwoordinhoud Hallo Hallo-bewerking.

![Rekenmachine-API][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a>Een bureaubladtoepassing toocall Hallo API configureren
de volgende procedure Hallo in Hallo video begint bij 16:30 en configureert u een eenvoudige bureaubladtoepassing toocall Hallo API. de eerste stap Hallo is tooregister Hallo bureaubladtoepassing in Azure AD en geef deze toegang toohello directory en toohello back-endservice. 18:25 is er een demonstratie van Hallo bureaubladtoepassing een bewerking op Hallo Rekenmachine-API aanroepen.

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a>Configureren van een JWT validatie beleid toopre-aanvragen toestaan
Hallo laatste procedure in Hallo video begint bij 20:48 en laat u zien hoe toouse hello [JWT valideren](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) beleid toopre-aanvragen door het Hallo-toegangstokens voor elke inkomende aanvraag valideren autoriseren. Hallo-aanvraag is niet gevalideerd door Hallo valideren JWT-beleid, Hallo-aanvraag wordt geblokkeerd door de API Management als back-end voor toohello niet wordt doorgestuurd.

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

Zie voor een andere demonstratie van configureren en gebruiken van dit beleid [Cloud hebben betrekking op aflevering 177: meer API Management-functies](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) en too13:50 vooruit. Snel toosee Hallo beleid dat is geconfigureerd in de beleidseditor Hallo doorsturen too15:00 en vervolgens too18:50 voor een demonstratie van een bewerking aanroepen vanuit de ontwikkelaarsportal Hallo zowel met als zonder Hallo verificatietoken vereist.

## <a name="next-steps"></a>Volgende stappen
* Bekijk meer [video's](https://azure.microsoft.com/documentation/videos/index/?services=api-management) over API Management.
* Voor andere manieren toosecure uw back-endservice Zie [wederzijdse certificaatverificatie](api-management-howto-mutual-certificates.md).

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md

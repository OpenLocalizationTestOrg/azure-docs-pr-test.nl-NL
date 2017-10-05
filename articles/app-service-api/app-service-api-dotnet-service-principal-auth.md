---
title: Verificatie van service-principal voor API Apps in Azure App Service | Microsoft Docs
description: Informatie over het beveiligen van een API-app in Azure App Service voor scenario's voor service-naar-service.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 7ca0bab2-1d29-4d51-b779-dce0edd34f8b
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 95653287546bbe358111ed16af0c30a53caff2b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Verificatie van service-principal voor API Apps in Azure App Service
## <a name="overview"></a>Overzicht
In dit artikel wordt uitgelegd hoe u App Service-verificatie voor *interne* toegang tot API-apps. Een interne scenario is waar u een API-app die u wilt worden alleen door uw eigen toepassingscode verbruikbare hebt. De aanbevolen manier om dit scenario implementeren in App Service wordt opgeroepen API-app beveiligen met Azure AD. U kunt de API-app met een bearer-token die u via Azure AD door het opgeven van de toepassings-id (service-principal) referenties beveiligde aanroepen. Zie voor alternatieven voor het gebruik van Azure AD de **authentication Service-naar-serviceconnector** sectie van de [overzicht van Azure App Service-authenticatie](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

In dit artikel leert u het volgende:

* Het gebruik van Azure Active Directory (Azure AD) voor een API-app beveiligen tegen niet-geverifieerde toegang.
* Klik hier voor meer informatie over het gebruiken van een beveiligde API-app van een API-app, web-app of mobiele app via Azure AD-referenties voor service-principal (app-identiteit). Zie voor meer informatie over het gebruiken van een logische app [uw aangepaste API gebruiken die worden gehost op App Service met Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).
* Hoe om ervoor te zorgen dat de beveiligde API-app kan niet worden aangeroepen vanuit een browser door aangemelde gebruikers.
* Hoe om ervoor te zorgen dat de beveiligde API-app kan alleen worden aangeroepen door een specifieke Azure AD service-principal.

Het artikel bestaat uit twee gedeelten:

* De [verificatie van de service-principal configureren in Azure App Service](#authconfig) sectie in het algemeen wordt uitgelegd hoe authentication configureren voor elke API-app en de beveiligde API-app gebruiken. Deze sectie is evenveel van toepassing op alle frameworks die worden ondersteund door App Service, waaronder .NET, Node.js en Java.
* Beginnen met de [u doorgaat met de zelfstudies .NET aan de slag](#tutorialstart) sectie de zelfstudie leidt u door een 'interne toegang'-scenario voor een .NET-voorbeeldtoepassing die is uitgevoerd in App Service configureren. 

## <a id="authconfig"></a>Verificatie van de service-principal in Azure App Service configureren
Deze sectie bevat algemene instructies die betrekking hebben op elke API-app. Voor specifieke stappen voor de voorbeeldtoepassing te doen lijst-.NET, gaat u naar [u doorgaat met de .NET API Apps zelfstudie reeks](#tutorialstart).

1. In de [Azure-portal](https://portal.azure.com/), gaat u naar de **instellingen** blade van de API-app die u wilt beveiligen en gaat u naar de **functies** sectie en klik op **verificatie / autorisatie**.
   
    ![Verificatie/autorisatie in Azure-portal](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. In de **verificatie / autorisatie** blade, klikt u op **op**.
3. In de **te ondernemen actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst, selecteer **aanmelden met Azure Active Directory** .
4. Onder **verificatieproviders**, selecteer **Azure Active Directory**.
   
    ![Verificatie/autorisatie-blade in Azure-portal](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Configureer de **Azure Active Directory-instellingen** blade Maak een nieuwe Azure AD-toepassing, of gebruik een bestaande Azure AD-toepassing als u al hebt die u wilt gebruiken.
   
    Interne scenario's omvatten doorgaans een API-app aanroepen van een API-app. U kunt afzonderlijke Azure AD-toepassingen voor elke API-app of slechts één Azure AD-toepassing.
   
    Zie voor gedetailleerde instructies voor deze blade [het configureren van uw App Service-toepassing voor het gebruik van Azure Active Directory-aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. Wanneer u met de blade verificatie provider configuratie bent klaar, klikt u op **OK**.
7. In de **verificatie / autorisatie** blade, klikt u op **opslaan**.
   
    ![Op Opslaan klikken](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

Wanneer dit wordt gedaan, App Service kunt alleen aanvragen van aanroepfuncties in de geconfigureerde Azure AD-tenant. Geen verificatie of autorisatie-code is vereist in de beveiligde API-app. De bearer-token wordt doorgegeven aan de API-app samen met vaak gebruikte claims in HTTP-headers en kunt u die informatie in de code te valideren dat verzoeken afkomstig van een bepaalde aanroeper, zoals een service-principal zijn lezen.

Deze functionaliteit verificatie werkt op dezelfde manier voor alle talen die App-service wordt ondersteund, waaronder .NET, Node.js en Java. 

#### <a name="how-to-consume-the-protected-api-app"></a>De beveiligde API-app gebruiken
De aanroeper moet een Azure AD-bearer-token met API-aanroepen opgeven. Als u een bearer-token met behulp van service-principal referenties, de aanroeper maakt gebruik van Active Directory Authentication Library (ADAL voor [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), of [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). Als u een token, bevat de code die ADAL-aanroepen adal de volgende informatie:

* De naam van uw Azure AD-tenant.
* De client-ID en clientgeheim (app-sleutel) van de Azure AD-app die is gekoppeld aan de aanroeper.
* De client-ID van de Azure AD-toepassing die is gekoppeld aan de beveiligde API-app. (Als slechts één Azure AD-toepassing wordt gebruikt, is dit de dezelfde client-ID als voor de aanroeper.)

Deze waarden zijn beschikbaar in de Azure AD's van de [klassieke Azure-portal](https://manage.windowsazure.com/).

Wanneer het token heeft aangeschaft, wordt het in de aanroeper bevat met HTTP-aanvragen in de autorisatie-header.  App Service valideert het token en kunnen de aanvragen voor het bereiken van de beveiligde API-app.

#### <a name="how-to-protect-the-api-app-from-access-by-users-in-the-same-tenant"></a>Het beveiligen van de API-app tegen toegang door gebruikers in dezelfde tenant
Voor gebruikers in dezelfde tenant-Bearer-tokens als geldig beschouwd voor het beveiligde API-app.  Als u wilt om ervoor te zorgen dat alleen een service-principal beveiligde API-app kunt aanroepen, moet u code toevoegen in de beveiligde API-app voor het valideren van de volgende claims uit het token:

* `appid`moet u de client-ID van de Azure AD-toepassing die is gekoppeld aan de aanroeper. 
* `oid`(`objectidentifier`) moet de service-principal-ID van de aanroepfunctie. 

App Service biedt ook de `objectidentifier` claim in de header X-MS-CLIENT-PRINCIPAL-ID.

### <a name="how-to-protect-the-api-app-from-browser-access"></a>Het beveiligen van de API-app van toegang tot de browser
Als u claims in de code in de beveiligde API-app niet valideren, en als u een afzonderlijke Azure AD-toepassing voor de beveiligde API-app, zorg ervoor dat de Azure AD-toepassing antwoord-URL is niet hetzelfde zijn als de basis-URL van de API-app. Als de antwoord-URL rechtstreeks naar de beveiligde API-app verwijst, kan een gebruiker in de dezelfde Azure AD-tenant Blader naar de API-app, aanmelden en is de API aanroepen.

## <a id="tutorialstart"></a>U kunt doorgaan de zelfstudie reeks .NET API-Apps
Als u de zelfstudie reeks Node.js of Java voor API-apps volgt, gaat u naar de [Vervolgstappen](#next-steps) sectie. 

De rest van dit artikel wordt de .NET API Apps zelfstudie reeks voortgezet en wordt ervan uitgegaan dat u hebt voltooid de [gebruiker verificatie zelfstudie](app-service-api-dotnet-user-principal-auth.md) en hebben de voorbeeldtoepassing die u uitvoert in Azure met de verificatie van de gebruiker is ingeschakeld.

## <a name="set-up-authentication-in-azure"></a>Verificatie in Azure instellen
In deze sectie u App Service zo configureren dat alleen HTTP-aanvragen dat kunt u de API app voor de gegevenslaag bereiken zijn degene die geldig Azure zijn AD-bearer-tokens. 

In de volgende sectie configureert u de API-app voor de middelste laag toepassing referenties te verzenden naar Azure AD, weer een bearer-token verkrijgen en de bearer-token verzenden naar de API app voor de gegevenslaag. Dit proces wordt weergegeven in het diagram.

![Service-verificatiediagram](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Als u problemen ondervindt tijdens de zelfstudie aanwijzingen, raadpleegt u de [probleemoplossing](#troubleshooting) sectie aan het einde van de zelfstudie. 

1. In de [Azure-portal](https://portal.azure.com/), gaat u naar de **instellingen** blade van de API-app die u voor de ToDoListDataAPI (gegevenslaag) API-app gemaakt en klik vervolgens op **instellingen**.
2. In de **instellingen** blade vinden de **functies** sectie en klik vervolgens op **verificatie / autorisatie**.
   
    ![Verificatie/autorisatie in Azure-portal](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. In de **verificatie / autorisatie** blade, klikt u op **op**.
4. In de **te ondernemen actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst, selecteer **aanmelden met Azure Active Directory**.
   
    Dit is de instelling zorgt ervoor dat de App-Service om ervoor te zorgen dat alleen aanvragen reach API-app geverifieerde. Voor aanvragen met geldig bearer-tokens, App Service de tokens langs wordt doorgegeven aan de API-app en HTTP-headers met veelgebruikte claims die informatie gemakkelijker om beschikbaar te maken aan uw code wordt gevuld.
5. Onder **verificatieproviders**, klikt u op **Azure Active Directory**.
   
    ![Verificatie/autorisatie-blade in Azure-portal](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. In de **Azure Active Directory-instellingen** blade, klikt u op **Express**.
   
    Met de **Express** optie Azure automatisch een AAD-toepassing maken in uw Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    U hoeft te maken van een tenant omdat elke Azure-account automatisch een heeft.
7. Onder **beheermodus**, klikt u op **nieuwe AD-App maken** als deze niet is geselecteerd.
   
    De portal kunt aansluiten de **App maken** invoervak met een standaardwaarde. Standaard is de Azure AD-toepassing naam hetzelfde zijn als de API-app. Als u liever, kunt u een andere naam.
   
    ![Azure AD-instellingen](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Opmerking**: als alternatief kunt u een Azure AD van één toepassing voor zowel de aanroepende API-app en de beveiligde API-app. Als u met deze alternatieve hebt gekozen, moet u niet de **nieuwe AD-App maken** optie hier omdat u al een Azure AD-toepassing eerder in de gebruiker authenticatie-zelfstudie hebt gemaakt. Voor deze zelfstudie gebruikt u Azure AD-toepassingen voor de aanroepende API-app en de beveiligde API-app.
8. Noteer de waarde die is in de **App maken** invoervak; u moet deze AAD-toepassing in de klassieke Azure portal later opzoeken.
9. Klik op **OK**.
10. In de **verificatie / autorisatie** blade, klikt u op **opslaan**.
    
    ![Op Opslaan klikken](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    App Service gemaakt in een Azure Active Directory-toepassing met **aanmeldings-URL** en **antwoord-URL** automatisch ingesteld op de URL van uw API-app. De laatste waarde kan gebruikers in uw AAD-tenant kunnen aanmelden en toegang tot de API-app.

### <a name="verify-that-the-api-app-is-protected"></a>Controleren of de API-app is beveiligd
1. Ga in een browser naar de URL van de API-app: in de **API-app** blade in de Azure-portal klikt u op de koppeling onder **URL**. 
   
    U wordt omgeleid naar een aanmeldingsscherm omdat niet-geverifieerde aanvragen zijn niet toegestaan voor het bereiken van de API-app. 
   
    Als uw browser naar de Swagger-gebruikersinterface gaat, kan al uw browser worden geregistreerd op--in dat geval open een InPrivate- of Incognito-venster en Ga naar de URL van de Swagger-gebruikersinterface.
2. Meld u aan met de referenties van een gebruiker in uw AAD-tenant.
   
   Wanneer u bent aangemeld, wordt de pagina 'is gemaakt' in de browser weergegeven.

## <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a>Het project ToDoListAPI om toegang te verkrijgen en stuurt het token Azure AD configureren
In deze sectie kunt u de volgende taken uitvoeren:

* Voeg code toe in de middelste laag API-app die gebruikmaakt van Azure AD-toepassing-referenties voor een token verkrijgen en verzenden met HTTP-aanvragen naar de API app voor de gegevenslaag.
* De referenties die u moet ophalen uit Azure AD.
* Voer de referenties in Azure App Service-runtime-omgevingsinstellingen in de middelste laag API-app. 

### <a name="configure-the-todolistapi-project-to-acquire-and-send-the-azure-ad-token"></a>Het project ToDoListAPI om toegang te verkrijgen en stuurt het token Azure AD configureren
De volgende wijzigingen aanbrengen in het project ToDoListAPI in Visual Studio.

1. Verwijder de opmerkingen in alle van de code in de *ServicePrincipal.cs* bestand.
   
    Dit is de code die gebruikmaakt van ADAL voor .NET te verkrijgen van de Azure AD-bearer-token.  Dit maakt gebruik van verschillende configuratiewaarden die u later in de Azure-runtime-omgeving hebt ingesteld. Dit is de code: 
   
        public static class ServicePrincipal
        {
            static string authority = ConfigurationManager.AppSettings["ida:Authority"];
            static string clientId = ConfigurationManager.AppSettings["ida:ClientId"];
            static string clientSecret = ConfigurationManager.AppSettings["ida:ClientSecret"];
            static string resource = ConfigurationManager.AppSettings["ida:Resource"];
   
            public static AuthenticationResult GetS2SAccessTokenForProdMSA()
            {
                return GetS2SAccessToken(authority, resource, clientId, clientSecret);
            }
   
            static AuthenticationResult GetS2SAccessToken(string authority, string resource, string clientId, string clientSecret)
            {
                var clientCredential = new ClientCredential(clientId, clientSecret);
                AuthenticationContext context = new AuthenticationContext(authority, false);
                AuthenticationResult authenticationResult = context.AcquireToken(
                    resource,
                    clientCredential);
                return authenticationResult;
            }
        }
   
    **Opmerking:** deze code vereist de ADAL voor .NET-NuGet-pakket (Microsoft.IdentityModel.Clients.ActiveDirectory) dat al is geïnstalleerd in het project. Als u dit project helemaal maakt, moet u dit pakket installeert. Dit pakket wordt niet automatisch geïnstalleerd door de sjabloon API app nieuw project.
2. In *domeincontrollers/ToDoListController*, herstel de code in de `NewDataAPIClient` methode waarmee het token wordt toegevoegd aan de HTTP-aanvragen in de autorisatie-header.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Implementeer het project ToDoListAPI. (Met de rechtermuisknop op het project en klik vervolgens op **publiceren > publiceren**.)
   
    Visual Studio implementeert het project en opent een browservenster met de basis-URL van de web-app. Hier ziet een fout 403-pagina normaal voor een poging is om naar een Web-API basis-URL vanuit een browser.
4. Sluit de browser.

### <a name="get-azure-ad-configuration-values"></a>Azure AD-configuratiewaarden ophalen
1. In de [klassieke Azure-portal](https://manage.windowsazure.com/), gaat u naar **Azure Active Directory**.
2. Op de **Directory** tabblad, klikt u op uw AAD-tenant.
3. Klik op **toepassingen > Mijn bedrijf eigenaar is van toepassingen**, en klik vervolgens op het vinkje.
4. Klik op de naam van de gebruiker die Azure voor u gemaakt wanneer u verificatie voor de ToDoListDataAPI (gegevenslaag) API-app hebt ingeschakeld in de lijst met toepassingen.
5. Klik op het tabblad **Configureren**.
6. Kopieer de **Client-ID** waarde en sla deze ergens kunt u dit uit later downloaden. 
7. In het Azure classic portal Ga terug naar de lijst met **toepassingen mijn bedrijf eigenaar is van**, en klik op de AAD-toepassing die u hebt gemaakt voor de middelste laag API-app ToDoListAPI (de tekst die u in de vorige zelfstudie hebt gemaakt, niet de tekst die u in deze zelfstudie hebt gemaakt).
8. Klik op het tabblad **Configureren**.
9. Kopieer de **Client-ID** waarde en sla deze ergens kunt u dit uit later downloaden.
10. Onder **sleutels**, selecteer **1 jaar** van de **Selecteer duur** vervolgkeuzelijst.
11. Klik op **Opslaan**.
    
     ![App-sleutel genereren](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Kopieer de sleutelwaarde en sla deze ergens die kunt u dit uit later downloaden.
    
     ![Kopiëren van de nieuwe app-sleutel](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-the-middle-tier-api-apps-runtime-environment"></a>Azure AD-instellingen configureren in de middelste laag API-app-runtime-omgeving
1. Ga naar de [Azure-portal](https://portal.azure.com/), en navigeer vervolgens naar de **API-App** blade voor de API-app die als host fungeert voor het project TodoListAPI (middelste laag).
2. Klik op **Instellingen > Toepassingsinstellingen**.
3. In de **appinstellingen** sectie, het toevoegen van de volgende sleutels en waarden:
   
   | **Sleutel** | IDA instantie: |
   | --- | --- |
   | **Waarde** |https://login.microsoftonline.com/ {uw Azure AD-tenant name} |
   | **Voorbeeld** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Sleutel** | IDA ClientId: |
   | --- | --- |
   | **Waarde** |Client-ID van de aanroepende toepassing (middelste laag - ToDoListAPI) |
   | **Voorbeeld** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **Sleutel** | IDA: ClientSecret |
   | --- | --- |
   | **Waarde** |App-sleutel van de aanroepende toepassing (middelste laag - ToDoListAPI) |
   | **Voorbeeld** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **Sleutel** | IDA Resource: |
   | --- | --- |
   | **Waarde** |Client-ID van de toepassing genoemd (gegevenslaag - ToDoListDataAPI) |
   | **Voorbeeld** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **Opmerking**: voor `ida:Resource`, zorg ervoor dat u de aangeroepen toepassing gebruiken **client-ID** en niet de **App ID URI**.
   
    `ida:ClientId`en `ida:Resource` zijn verschillende waarden voor deze zelfstudie omdat u werkt met afzonderlijke applicaations Azure AD voor de middelste laag en de gegevenslaag. Als u één Azure AD-toepassing voor de aanroepende API-app en de beveiligde API-app, gebruikt u dezelfde waarde in beide `ida:ClientId` en `ida:Resource`.
   
    De code gebruikt ConfigurationManager ophalen van deze waarden, zodat kan worden opgeslagen in Web.config-bestand van het project of in de Azure-runtime-omgeving. Terwijl een ASP.NET-toepassing in Azure App Service wordt uitgevoerd, overschrijven de instellingen voor automatisch instellingen uit Web.config. Omgevingsinstellingen zijn doorgaans een [veiliger manier voor het opslaan van vertrouwelijke gegevens vergeleken met een Web.config-bestand](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. Klik op **Opslaan**.
   
    ![Op Opslaan klikken](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-the-application"></a>De toepassing testen
1. Ga in een browser naar de HTTPS-URL van de AngularJS-front-end web-app.
2. Klik op de **To Do List** tabblad en meld u aan met referenties voor een gebruiker in uw Azure AD-tenant. 
3. Toevoegen van taakitems om te controleren of de toepassing werkt.
   
    ![Takenlijstpagina](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Als de toepassing niet werkt zoals verwacht, Controleer alle instellingen die u hebt ingevoerd in de Azure-portal. Als u alle instellingen correct lijken, raadpleegt u de [probleemoplossing](#troubleshooting) verderop in deze zelfstudie.

## <a name="protect-the-api-app-from-browser-access"></a>De API-app beveiligen tegen toegang tot de browser
Voor deze zelfstudie die u hebt gemaakt een afzonderlijke Azure AD-toepassing voor de ToDoListDataAPI (gegevenslaag) API-app. Als u hebt gezien, wanneer de App Service een AAD-toepassing maakt, configureert het AAD-toepassing op een manier waarmee een gebruiker gaat u naar de API-app-URL in een browser en meld u aan. Dit betekent dat het is mogelijk voor gebruikers in uw Azure AD-tenant, niet alleen een service-principal, voor toegang tot de API. 

Als u voorkomen dat toegang tot de browser wilt zonder de code schrijven in de beveiligde API-app, kunt u de **antwoord-URL** in de AAD-toepassing zodat deze van de API-app verschilt basis-URL. 

### <a name="disable-browser-access"></a>Toegang tot de browser uitschakelen
1. In de klassieke portal **configureren** voor de AAD-toepassing die is gemaakt voor de TodoListService en wijzig de waarde in de **antwoord-URL** veld zodat het een geldige URL, maar niet de API-app-URL.
2. Klik op **Opslaan**.

### <a name="verify-browser-access-no-longer-works"></a>Controleer of toegang tot de browser niet meer werkt
Eerder gecontroleerd dat u naar de API-app-URL vanuit een browser gaat door met de referenties van een afzonderlijke gebruiker aanmeldt. In deze sectie, controleert u of dit is niet langer mogelijk. 

1. In een nieuw browservenster en gaat u naar de URL van de API-app opnieuw.
2. Registreren in wanneer u daarom wordt gevraagd.
3. Aanmelding is geslaagd, maar leidt tot een foutpagina.
   
    U kunt de AAD-app hebt geconfigureerd, zodat gebruikers in de AAD-tenant kunnen niet aanmelden en toegang de API vanuit een browser tot. U kunt nog steeds toegang tot de API-app met behulp van een token voor principal op service, waarmee u controleren kunt door te gaan naar de web-app-URL en meer taakitems toe te voegen.

## <a name="restrict-access-to-a-particular-service-principal"></a>Beperk de toegang tot een bepaalde service-principal
Momenteel aanroeper die een token kan krijgen voor een gebruiker of service-principal in uw Azure AD-tenant de TodoListDataAPI (gegevenslaag) API-app kunt aanroepen. Het is raadzaam om ervoor te zorgen dat de API app voor de gegevenslaag accepteert alleen aanroepen vanuit de app TodoListAPI (middelste laag) API, en alleen vanuit een bepaalde service-principal. 

U kunt deze beperkingen toevoegen door toe te voegen code voor het valideren van de `appid` en `objectidentifier` claims op binnenkomende oproepen.

Voor deze zelfstudie kunt u de code te valideren en app-ID en service-principal-ID rechtstreeks in uw domeincontroller acties plaatsen.  Alternatieven zijn gebruik van een aangepaste `Authorize` kenmerk of het uitvoeren van deze validatie het opstarten (bijvoorbeeld OWIN middleware) takenreeksen. Zie voor een voorbeeld van de laatste [deze voorbeeldtoepassing](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

De volgende wijzigingen aanbrengen in het project TodoListDataAPI.

1. Open de *Controllers/TodoListController.cs* bestand.
2. Verwijder de opmerkingen in de regels die ingesteld `trustedCallerClientId` en `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Herstel de code in de methode CheckCallerId. Deze methode is aangeroepen aan het begin van elke actiemethode in de controller. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "The appID or service principal ID is not the expected value." });
            }
        }
4. Implementeer het project ToDoListDataAPI in Azure App Service opnieuw.
5. In de browser, Ga naar HTTPS-URL van de AngularJS-front-end web app en in de startpagina klikt u op de **To Do List** tabblad.
   
    De toepassing werkt niet omdat aanroepen naar de back-end mislukken. De nieuwe code is werkelijke appid en objectidentifier controleren maar nog geen deze de juiste waarden om te controleren ze tegen. De browser die de Console hulpprogramma's voor ontwikkelaars rapporteert dat de server een 401 HTTP-fout retourneert.
   
    ![Fout in Developer Tools Console](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    In de volgende stappen configureert u de verwachte waarden.
6. Met Azure AD PowerShell, haal de waarde van de service-principal voor de Azure AD-toepassing die u hebt gemaakt voor het project TodoListWebApp.
   
    a. Zie voor instructies over hoe u Azure PowerShell installeren en verbinding maken met uw abonnement, [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md).
   
    b. Als u een lijst met de service-principals, uitvoeren van de `Login-AzureRmAccount` opdracht en vervolgens de `Get-AzureRmADServicePrincipal` opdracht.
   
    c. De object-id vinden voor de service-principal van de toepassing TodoListAPI en opslaan in een locatie die u later kunt kopiëren uit.
7. Navigeer naar de blade API-app voor de API-app die u hebt geïmplementeerd op het project ToDoListDataAPI in de Azure portal.
8. Klik op **instellingen > Toepassingsinstellingen**.
9. In de **appinstellingen** sectie, het toevoegen van de volgende sleutels en waarden:
   
   | **Sleutel** | TODO:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Waarde** |Service-principal-id van het aanroepen van toepassing |
   | **Voorbeeld** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Sleutel** | TODO:TrustedCallerClientId |
   | --- | --- |
   | **Waarde** |Client-ID van het aanroepen van de toepassing - gekopieerd uit de TodoListAPI Azure AD-toepassing |
   | **Voorbeeld** |960adec2-b74a-484a-960adec2-b74a-484a |
10. Klik op **Opslaan**.
    
     ![Op Opslaan klikken](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. Klik in de startpagina en in uw browser, Ga terug naar de web-app-URL op de **To Do List** tabblad.
    
     Deze tijd de toepassing werkt zoals verwacht, omdat de aanroeper vertrouwde app-ID en service-principal-ID zijn de verwachte waarden.
    
     ![Takenlijstpagina](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-the-projects-from-scratch"></a>Het bouwen van de projecten maken
De twee Web API-projecten zijn gemaakt met behulp van de **Azure API-App** project sjabloon en de waarden van standaard domeincontroller vervangen door een ToDoList-controller. Voor het verkrijgen van Azure AD-service-principal tokens in het project ToDoListAPI de [Active Directory Authentication Library (ADAL) voor .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet-pakket is geïnstalleerd.

Zie voor meer informatie over het maken van een AngularJS-toepassing voor één pagina met een Web-API-back-end zoals ToDoListAngular [handen op Lab: bouwen van een enkele toepassing pagina WACHTWOORDVERIFICATIE met ASP.NET Web API en Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Zie voor meer informatie over het toevoegen van Azure AD-verificatiecode [beveiligen AngularJS één pagina Apps met Azure AD](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Problemen oplossen
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Zorg ervoor dat u en niet door elkaar ToDoListAPI (middelste laag) ToDoListDataAPI (gegevenslaag). Bijvoorbeeld: in deze zelfstudie u verificatie toevoegen aan de gegevens laag API-app **, maar de app-sleutel moet afkomstig zijn van de Azure AD-toepassing die u hebt gemaakt voor de middelste laag API-app**.

## <a name="next-steps"></a>Volgende stappen
Dit is de laatste zelfstudie in de reeks API-Apps. 

Zie de volgende bronnen voor meer informatie over Azure Active Directory.

* [Azure AD ontwikkelaarshandleiding](http://aka.ms/aaddev)
* [Azure AD-scenario 's](http://aka.ms/aadscenarios)
* [Azure AD-voorbeelden](http://aka.ms/aadsamples)
  
    De [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) voorbeeld is vergelijkbaar met wat wordt weergegeven in deze zelfstudie, maar zonder verificatie van App Service.

Voor informatie over andere manieren voor het implementeren van Visual Studio-projecten in API-apps met behulp van Visual Studio of [implementatie automatiseren](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) van een [broncodebeheersysteem](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), Zie [het implementeren van een Azure App Service-app](../app-service-web/web-sites-deploy.md).


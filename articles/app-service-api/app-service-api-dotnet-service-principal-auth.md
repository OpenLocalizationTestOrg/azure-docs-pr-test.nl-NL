---
title: aaaService verificatie voor API Apps in Azure App Service | Microsoft Docs
description: Meer informatie over hoe tooprotect een API-app in Azure App Service voor scenario's voor service-naar-service.
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
ms.openlocfilehash: 94d9ee11f38293df4a2fd815ef02c59cc6defed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-principal-authentication-for-api-apps-in-azure-app-service"></a>Verificatie van service-principal voor API Apps in Azure App Service
## <a name="overview"></a>Overzicht
Dit artikel wordt uitgelegd hoe toouse App Service-verificatie voor *interne* toegang tot tooAPI apps. Een interne scenario is waar u een API-app die u toobe verbruikbare alleen door uw eigen toepassingscode wilt. Hallo aanbevolen manier tooimplement dit scenario in App Service toouse Azure AD tooprotect Hallo heet API-app. U kunt Hallo beveiligd API-app met een bearer-token die u via Azure AD door het opgeven van de toepassings-id (service-principal) referenties aanroepen. Zie voor alternatieven toousing Azure AD, Hallo **authentication Service-naar-service** sectie Hallo [overzicht van Azure App Service-authenticatie](../app-service/app-service-authentication-overview.md#service-to-service-authentication).

In dit artikel leert u het volgende:

* Hoe toouse Azure Active Directory (Azure AD) tooprotect een API-app van niet-geverifieerde toegang.
* Hoe tooconsume een beveiligde API-app uit een API-app, web-app of mobiele app met behulp van Azure AD-referenties voor service-principal (app-identiteit). Voor informatie over het tooconsume van een logische app, Zie [uw aangepaste API gebruiken die worden gehost op App Service met Logic apps](../logic-apps/logic-apps-custom-hosted-api.md).
* Hoe toomake zorgen dat Hallo beschermd API-app kan niet worden aangeroepen vanuit een browser door gebruikers zijn aangemeld.
* Hoe toomake zorgen dat Hallo beschermd API-app kan alleen worden aangeroepen door een specifieke service-principal voor Azure AD.

Hallo artikel bestaat uit twee gedeelten:

* Hallo [hoe tooconfigure service-principal verificatie in Azure App Service](#authconfig) sectie wordt uitgelegd hoe u algemene tooconfigure verificatie voor een API-app, en hoe tooconsume Hallo beveiligd API-app. Deze sectie is evenveel van toepassing tooall frameworks die worden ondersteund door App Service, waaronder .NET, Node.js en Java.
* Beginnen met Hallo [u doorgaat zelfstudies .NET-aan de slag Hallo](#tutorialstart) sectie Hallo zelfstudie leidt u door een 'interne toegang'-scenario voor een .NET-voorbeeldtoepassing die is uitgevoerd in App Service configureren. 

## <a id="authconfig"></a>Hoe tooconfigure service-principal verificatie in Azure App Service
Deze sectie bevat algemene instructies die van toepassing zijn tooany API-app. Ga te voor stappen specifieke toohello tooDo lijst .NET-voorbeeldtoepassing[u doorgaat Hallo .NET API Apps-zelfstudie reeks](#tutorialstart).

1. In Hallo [Azure-portal](https://portal.azure.com/), navigeer toohello **instellingen** blade van Hallo API-app die u tooprotect wilt en gaat u naar Hallo **functies** sectie en klikt u op **Verificatie / autorisatie**.
   
    ![Verificatie/autorisatie in Azure-portal](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. In Hallo **verificatie / autorisatie** blade, klikt u op **op**.
3. In Hallo **tootake actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst, selecteer **aanmelden met Azure Active Directory** .
4. Onder **verificatieproviders**, selecteer **Azure Active Directory**.
   
    ![Verificatie/autorisatie-blade in Azure-portal](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. Hallo configureren **Azure Active Directory-instellingen** blade toocreate een nieuwe Azure AD-toepassing, of gebruik een bestaande Azure AD-toepassing als u al hebt dat u wilt dat toouse.
   
    Interne scenario's omvatten doorgaans een API-app aanroepen van een API-app. U kunt afzonderlijke Azure AD-toepassingen voor elke API-app of slechts één Azure AD-toepassing.
   
    Zie voor gedetailleerde instructies voor deze blade [hoe tooconfigure uw App Service-toepassing toouse Azure Active Directory-aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
6. Wanneer u met de Hallo verificatie provider configuratie blade bent klaar, klikt u op **OK**.
7. In Hallo **verificatie / autorisatie** blade, klikt u op **opslaan**.
   
    ![Op Opslaan klikken](./media/app-service-api-dotnet-service-principal-auth/authsave.png)

Wanneer dit wordt gedaan, staat App Service alleen aanvragen van aanroepfuncties in Azure AD-tenant Hallo geconfigureerd. Geen verificatie of autorisatie-code is vereist in Hallo beveiligd API-app. Hallo bearer-token wordt doorgegeven toohello API-app samen met veelgebruikte claims in HTTP-headers en kunt u deze informatie weer in code toovalidate die aanvragen afkomstig van een bepaalde aanroeper, zoals een service-principal zijn lezen.

Deze functionaliteit verificatie werkt Hallo dezelfde manier voor alle talen die App-service ondersteunt, zoals .NET, Node.js en Java. 

#### <a name="how-tooconsume-hello-protected-api-app"></a>Hoe tooconsume Hallo beveiligd API-app
Hallo aanroeper moet een Azure AD-bearer-token met API-aanroepen opgeven. tooget bearer-token met behulp van service-principal referenties, Hallo aanroeper gebruikmaakt van Active Directory Authentication Library (ADAL voor [.NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory), [Node.js](https://github.com/AzureAD/azure-activedirectory-library-for-nodejs), of [Java](https://github.com/AzureAD/azure-activedirectory-library-for-java)). een token tooget, Hallo-code die ADAL-aanroepen biedt tooADAL Hallo volgende informatie:

* Hallo-naam van uw Azure AD-tenant.
* Hallo-ID en client clientgeheim (app-sleutel) van hello Azure AD-app die is gekoppeld aan de aanroeper Hallo.
* client-ID van Azure AD-toepassing die is gekoppeld aan Hallo HALLO hallo beveiligd API-app. (Als slechts één Azure AD-toepassing wordt gebruikt, dit is Hallo dezelfde client-ID als een voor de aanroeper Hallo Hallo.)

Deze waarden zijn beschikbaar in hello Azure AD-pagina's van Hallo [klassieke Azure-portal](https://manage.windowsazure.com/).

Zodra het Hallo-token is aangeschaft, Hallo aanroeper opgenomen in de met HTTP-aanvragen in Hallo autorisatie-header.  App Service Hallo token valideert en kunnen Hallo aanvragen tooreach Hallo beveiligd API-app.

#### <a name="how-tooprotect-hello-api-app-from-access-by-users-in-hello-same-tenant"></a>Hoe tooprotect Hallo API-app tegen toegang door gebruikers in Hallo die dezelfde tenant
Bearer-tokens voor gebruikers in dezelfde tenant worden beschouwd als geldig voor Hallo Hallo beveiligd API-app.  Als u wilt dat tooensure die alleen een service-principal kunt aanroepen Hallo beveiligde API-app, het toevoegen van de code in Hallo beschermd API app toovalidate Hallo claims van Hallo-token te volgen:

* `appid`client-ID van hello Azure AD-toepassing die is gekoppeld aan de aanroeper Hallo Hallo moet. 
* `oid`(`objectidentifier`) moet Hallo service principal-ID van de aanroepfunctie Hallo. 

App Service biedt ook Hallo `objectidentifier` claim in de header Hallo X-MS-CLIENT-PRINCIPAL-ID.

### <a name="how-tooprotect-hello-api-app-from-browser-access"></a>Hoe tooprotect Hallo API-app van toegang tot de browser
Als u claims in de code in Hallo beveiligd API-app niet valideren, en als u een afzonderlijke Azure AD-toepassing voor Hallo beveiligd API-app, zorg ervoor dat hello Azure AD-toepassing antwoord-URL is Hallo niet hetzelfde als het Hallo-API-app basis-URL. Als Hallo antwoord-URL rechtstreeks toohello beveiligd API-app verwijst, kan een gebruiker in Hallo dezelfde Azure AD-tenant toohello API-app bladeren, aanmelden en roepen Hallo-API.

## <a id="tutorialstart"></a>U kunt doorgaan zelfstudie Hallo .NET API Apps-reeks
Als u Hallo Node.js of Java zelfstudie reeksen voor API-apps volgt, gaat u verder toohello [Vervolgstappen](#next-steps) sectie. 

Hallo rest van dit artikel wordt voortgezet Hallo .NET API Apps-zelfstudie reeks en wordt ervan uitgegaan dat u Hallo hebt voltooid [gebruiker verificatie zelfstudie](app-service-api-dotnet-user-principal-auth.md) en Hallo-voorbeeldtoepassing die is uitgevoerd in Azure met gebruikersverificatie hebben ingeschakeld.

## <a name="set-up-authentication-in-azure"></a>Verificatie in Azure instellen
In deze sectie u App Service zo configureren dat alleen HTTP-aanvragen kunt u tooreach Hallo API app voor de gegevenslaag Hallo zijn Hallo waarden die u geldige Azure hebt AD-bearer-tokens. 

In Hallo volgende sectie, Hallo middelste laag API app toosend toepassing referenties tooAzure AD configureren, weer een bearer-token verkrijgen en Hallo bearer-token toohello gegevens laag API-app verzenden. Dit proces wordt weergegeven in Hallo-diagram.

![Service-verificatiediagram](./media/app-service-api-dotnet-service-principal-auth/appdiagram.png)

Als u problemen bij de volgende zelfstudie Hallo-instructies, Zie Hallo [probleemoplossing](#troubleshooting) sectie aan einde van de zelfstudie Hallo Hallo. 

1. In Hallo [Azure-portal](https://portal.azure.com/), navigeer toohello **instellingen** blade van Hallo API-app die u voor Hallo ToDoListDataAPI (gegevenslaag) API-app gemaakt en klik vervolgens op **instellingen**.
2. In Hallo **instellingen** blade, zoeken Hallo **functies** sectie en klik vervolgens op **verificatie / autorisatie**.
   
    ![Verificatie/autorisatie in Azure-portal](./media/app-service-api-dotnet-user-principal-auth/features.png)
3. In Hallo **verificatie / autorisatie** blade, klikt u op **op**.
4. In Hallo **tootake actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst, selecteer **aanmelden met Azure Active Directory**.
   
    Dit is Hallo instelling zorgt ervoor dat de App Service-tooensure die alleen aanvragen reach Hallo API-app geverifieerde. Voor aanvragen met geldig bearer-tokens, App Service doorgegeven Hallo tokens langs toohello API-app en HTTP-headers met veelgebruikte claims toomake gevuld die informatie gemakkelijker beschikbaar tooyour code.
5. Onder **verificatieproviders**, klikt u op **Azure Active Directory**.
   
    ![Verificatie/autorisatie-blade in Azure-portal](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
6. In Hallo **Azure Active Directory-instellingen** blade, klikt u op **Express**.
   
    Hello **Express** optie Azure automatisch een AAD-toepassing maken in uw Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    U hebt geen toocreate een tenant, omdat elke Azure-account automatisch een heeft.
7. Onder **beheermodus**, klikt u op **nieuwe AD-App maken** als deze niet is geselecteerd.
   
    Hallo-portal kunt aansluiten Hallo **App maken** invoervak met een standaardwaarde. Naam standaard hello Azure AD-toepassing hello dezelfde als Hallo API-app. Als u liever, kunt u een andere naam.
   
    ![Azure AD-instellingen](./media/app-service-api-dotnet-service-principal-auth/aadsettings.png)
   
    **Opmerking**: als alternatief kunt u een Azure AD van één toepassing voor zowel Hallo aanroepen API-app en Hallo beveiligd API-app. Als u met deze alternatieve hebt gekozen, moet u niet Hallo **nieuwe AD-App maken** optie hier omdat u al een Azure AD-toepassing eerder in Hallo gebruiker verificatie zelfstudie hebt gemaakt. Voor deze zelfstudie maakt u afzonderlijke Azure AD-toepassingen voor de aanroepen van API-app en Hallo Hallo beveiligd API-app.
8. Maak een notitie van Hallo waarde in Hallo **App maken** invoervak; u moet deze AAD-toepassing in opzoeken Hallo klassieke Azure-portal later.
9. Klik op **OK**.
10. In Hallo **verificatie / autorisatie** blade, klikt u op **opslaan**.
    
    ![Op Opslaan klikken](./media/app-service-api-dotnet-service-principal-auth/saveauth.png)
    
    App Service gemaakt in een Azure Active Directory-toepassing met **aanmeldings-URL** en **antwoord-URL** toohello-URL van uw API-app worden automatisch ingesteld. de laatste waarde Hallo kan gebruikers in uw AAD-tenant toolog in en toegang Hallo API-app.

### <a name="verify-that-hello-api-app-is-protected"></a>Controleer of dat die Hallo API-app is beveiligd
1. Ga in een browser toohello-URL van Hallo API-app: in Hallo **API-app** blade in hello Azure-portal, klikt u op de koppeling onder Hallo **URL**. 
   
    U bent omgeleide tooa aanmeldingsscherm omdat niet-geverifieerde aanvragen tooreach Hallo API-app niet zijn toegestaan. 
   
    Als uw browser Ga toohello Swagger-gebruikersinterface, uw browser mogelijk al aangemeld--in dat geval open een InPrivate- of Incognito-venster en ga toohello Swagger-gebruikersinterface-URL.
2. Meld u aan met de referenties van een gebruiker in uw AAD-tenant.
   
   Wanneer u bent aangemeld, wordt de pagina 'gemaakt' hello weergegeven in Hallo browser.

## <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Hallo ToDoListAPI-project tooacquire configureren en stuurt hello Azure AD-token
In deze sectie u Hallo volgende taken:

* Voeg code toe in Hallo middelste laag API-app die gebruikmaakt van Azure AD-toepassing referenties tooacquire een token en verzenden dat met HTTP-aanvragen API-app voor de laag toohello gegevens.
* Hallo-referenties die u moet ophalen uit Azure AD.
* Geef referenties op Hallo in Azure App Service runtime omgevingsinstellingen in Hallo middelste laag API-app. 

### <a name="configure-hello-todolistapi-project-tooacquire-and-send-hello-azure-ad-token"></a>Hallo ToDoListAPI-project tooacquire configureren en stuurt hello Azure AD-token
Controleer Hallo volgende wijzigingen in Hallo ToDoListAPI-project in Visual Studio.

1. Verwijder de opmerkingen in alle code in Hallo Hallo *ServicePrincipal.cs* bestand.
   
    Dit is Hallo-code die gebruikmaakt van ADAL voor .NET tooacquire hello Azure AD bearer-token.  Dit maakt gebruik van verschillende configuratiewaarden die u later in hello Azure runtime-omgeving hebt ingesteld. Dit is Hallo code: 
   
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
   
    **Opmerking:** deze code vereist Hallo ADAL voor .NET-NuGet-pakket (Microsoft.IdentityModel.Clients.ActiveDirectory) dat al is geïnstalleerd in Hallo-project. Als u dit project helemaal maakt, hebt u tooinstall dit pakket. Dit pakket wordt niet automatisch geïnstalleerd door Hallo API-app-nieuw project-sjabloon.
2. In *domeincontrollers/ToDoListController*, Opmerking verwijderen Hallo-code in Hallo `NewDataAPIClient` methode waarmee Hallo token tooHTTP aanvragen in Hallo autorisatie-header worden toegevoegd.
   
        client.HttpClient.DefaultRequestHeaders.Authorization =
            new AuthenticationHeaderValue("Bearer", ServicePrincipal.GetS2SAccessTokenForProdMSA().AccessToken);
3. Hallo ToDoListAPI-project implementeert. (Met de rechtermuisknop op het Hallo-project en klik vervolgens op **publiceren > publiceren**.)
   
    Visual Studio implementeert Hallo-project en basis-URL in een browser toohello van web-app wordt geopend. Hier ziet een fout 403-pagina normaal voor een poging toogo tooa Web API basis-URL vanuit een browser is.
4. De browser sluiten Hallo.

### <a name="get-azure-ad-configuration-values"></a>Azure AD-configuratiewaarden ophalen
1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), gaat u te**Azure Active Directory**.
2. Op Hallo **Directory** tabblad, klikt u op uw AAD-tenant.
3. Klik op **toepassingen > Mijn bedrijf eigenaar is van toepassingen**, en klik vervolgens op het vinkje Hallo.
4. Klik op Hallo naam Hallo die Azure voor u gemaakt wanneer u verificatie voor Hallo ToDoListDataAPI (gegevenslaag) API-app hebt ingeschakeld in de lijst met toepassingen Hallo.
5. Klik op Hallo **configureren** tabblad.
6. Kopiëren Hallo **Client-ID** waarde en sla deze ergens kunt u dit uit later downloaden. 
7. In de klassieke Azure-portal Hallo terug toohello lijst met **toepassingen mijn bedrijf eigenaar is van**, en klik op Hallo AAD-toepassing die u hebt gemaakt voor Hallo middelste laag API-app ToDoListAPI (Hallo dat u niet in de vorige zelfstudie Hallo hebt gemaakt Hallo dat die u in deze zelfstudie hebt gemaakt).
8. Klik op Hallo **configureren** tabblad.
9. Kopiëren Hallo **Client-ID** waarde en sla deze ergens kunt u dit uit later downloaden.
10. Onder **sleutels**, selecteer **1 jaar** van Hallo **Selecteer duur** vervolgkeuzelijst.
11. Klik op **Opslaan**.
    
     ![App-sleutel genereren](./media/app-service-api-dotnet-service-principal-auth/genkey.png)
12. Kopieer de sleutelwaarde Hallo en sla deze ergens die kunt u dit uit later downloaden.
    
     ![Kopiëren van de nieuwe app-sleutel](./media/app-service-api-dotnet-service-principal-auth/genkeycopy.png)

### <a name="configure-azure-ad-settings-in-hello-middle-tier-api-apps-runtime-environment"></a>Azure AD-instellingen configureren in Hallo middelste laag API app runtime-omgeving
1. Ga toohello [Azure-portal](https://portal.azure.com/), en navigeert u vervolgens toohello **API-App** blade voor Hallo API-app die als host fungeert voor project van Hallo TodoListAPI (middelste laag).
2. Klik op **Instellingen > Toepassingsinstellingen**.
3. In Hallo **appinstellingen** sectie, Hallo volgende sleutels en waarden toevoegen:
   
   | **Sleutel** | IDA instantie: |
   | --- | --- |
   | **Waarde** |https://login.microsoftonline.com/ {uw Azure AD-tenant name} |
   | **Voorbeeld** |https://login.microsoftonline.com/contoso.onmicrosoft.com |
   
   | **Sleutel** | IDA ClientId: |
   | --- | --- |
   | **Waarde** |Client-ID van Hallo aanroepen van toepassing (middelste laag - ToDoListAPI) |
   | **Voorbeeld** |960adec2-b74a-484a-960adec2-b74a-484a |
   
   | **Sleutel** | IDA: ClientSecret |
   | --- | --- |
   | **Waarde** |App-sleutel Hallo aanroepen van toepassing (middelste laag - ToDoListAPI) |
   | **Voorbeeld** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
   | **Sleutel** | IDA Resource: |
   | --- | --- |
   | **Waarde** |Client-ID van aangeroepen toepassing hello (gegevenslaag - ToDoListDataAPI) |
   | **Voorbeeld** |e65e8fc9-5f6b-48e8-e65e8fc9-5f6b-48e8 |
   
    **Opmerking**: voor `ida:Resource`, zorg ervoor dat u gebruikt naam van de toepassing hello **client-ID** en niet de **App ID URI**.
   
    `ida:ClientId`en `ida:Resource` zijn verschillende waarden voor deze zelfstudie omdat u werkt met afzonderlijke applicaations Azure AD voor de middelste laag Hallo en de gegevenslaag. Als u één Azure AD-toepassing voor het aanroepen van API-app en Hallo Hallo beveiligd API-app, gebruikt u dezelfde in beide waarde Hallo `ida:ClientId` en `ida:Resource`.
   
    Hallo code gebruikt ConfigurationManager tooget deze waarden, zodat kan worden opgeslagen in Web.config-bestand van het project Hallo of in hello Azure runtime-omgeving. Terwijl een ASP.NET-toepassing in Azure App Service wordt uitgevoerd, overschrijven de instellingen voor automatisch instellingen uit Web.config. Omgevingsinstellingen zijn doorgaans een [tooa Web.config-bestand ten opzichte van een veiliger manier toostore gevoelige informatie](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).
4. Klik op **Opslaan**.
   
    ![Op Opslaan klikken](./media/app-service-api-dotnet-service-principal-auth/appsettings.png)

### <a name="test-hello-application"></a>Hallo toepassing testen
1. Ga in een browser toohello HTTPS-URL van Hallo AngularJS-front-end web-app.
2. Klik op Hallo **tooDo lijst** tabblad en meld u aan met referenties voor een gebruiker in uw Azure AD-tenant. 
3. Taak items tooverify die toepassing hello werkt toevoegen.
   
    ![pagina van de lijst met tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)
   
    Als de toepassing hello niet werkt zoals verwacht, Controleer alle Hallo-instellingen die u hebt ingevoerd in hello Azure-portal. Als alle Hallo instellingen toobe juist wordt weergegeven, Zie Hallo [probleemoplossing](#troubleshooting) verderop in deze zelfstudie.

## <a name="protect-hello-api-app-from-browser-access"></a>Hallo-API-app beveiligen tegen toegang tot de browser
Voor deze zelfstudie die u hebt gemaakt een afzonderlijke Azure AD-toepassing voor Hallo ToDoListDataAPI (gegevenslaag) API-app. Als u hebt gezien, wanneer de App Service een AAD-toepassing maakt configureert het Hallo-AAD-toepassing op een manier die een gebruiker toogo toohello van API-app-URL in een browser en meld schakelt op. Dit betekent dat het is mogelijk voor gebruikers in uw Azure AD-tenant, niet alleen een service-principal, tooaccess Hallo API. 

Als u toegang tot de tooprevent browser wilt zonder code schrijven in Hallo API-app beveiligd, kunt u Hallo **antwoord-URL** in AAD-toepassing hello zodat deze van Hallo API-app verschilt basis-URL. 

### <a name="disable-browser-access"></a>Toegang tot de browser uitschakelen
1. In Hallo klassieke portal **configureren** voor Hallo AAD-toepassing die is gemaakt voor Hallo TodoListService en wijzig de waarde in Hallo Hallo **antwoord-URL** zodat het een geldige URL, maar niet Hallo API-app van veld DE URL.
2. Klik op **Opslaan**.

### <a name="verify-browser-access-no-longer-works"></a>Controleer of toegang tot de browser niet meer werkt
Eerder gecontroleerd dat kunt u toohello API-app-URL gaan vanuit een browser door met de referenties van een afzonderlijke gebruiker aanmeldt. In deze sectie, controleert u of dit is niet langer mogelijk. 

1. Ga toohello-URL van de API-app Hallo opnieuw in een nieuw browservenster.
2. Aanmelden bij gevraagd toodo dus.
3. Aanmelding is geslaagd, maar tooan foutpagina leidt.
   
    U kunt Hallo AAD-app hebt geconfigureerd, zodat gebruikers in Hallo AAD-tenant kunnen niet aanmelden en toegang Hallo API vanuit een browser. U kunt nog steeds toegang tot Hallo API-app met behulp van een token voor principal op service, waarmee u controleren kunt door te gaan toohello van web-app-URL en meer taakitems toe te voegen.

## <a name="restrict-access-tooa-particular-service-principal"></a>Beperken van toegang tooa bepaalde service-principal
Momenteel aanroeper die een token kan krijgen voor een gebruiker of service-principal in uw Azure AD-tenant hello TodoListDataAPI (gegevenslaag) API-app kunt aanroepen. Hier kunt u ervoor dat Hallo API app voor de gegevenslaag accepteert alleen aanroepen van Hallo TodoListAPI (middelste laag) API-app, en alleen vanuit een bepaalde service-principal toomake. 

U kunt deze beperkingen toevoegen door toe te voegen code toovalidate hello `appid` en `objectidentifier` claims op binnenkomende oproepen.

Voor deze zelfstudie plaatsen u Hallo-code die app-ID en de service-principal-ID rechtstreeks in uw domeincontroller acties worden gevalideerd.  Alternatieven zijn toouse een aangepaste `Authorize` kenmerk of toodo deze validatie in uw takenreeksen opstarten (bijvoorbeeld OWIN middleware). Zie voor een voorbeeld van de laatste Hallo [deze voorbeeldtoepassing](https://github.com/mohitsriv/EasyAuthMultiTierSample/blob/master/MyDashDataAPI/Startup.cs). 

Hallo na wijzigingen toohello TodoListDataAPI-project maken

1. Open Hallo *Controllers/TodoListController.cs* bestand.
2. Verwijder de opmerkingen in Hallo-regels die ingesteld `trustedCallerClientId` en `trustedCallerServicePrincipalId`.
   
        private static string trustedCallerClientId = ConfigurationManager.AppSettings["todo:TrustedCallerClientId"];
        private static string trustedCallerServicePrincipalId = ConfigurationManager.AppSettings["todo:TrustedCallerServicePrincipalId"];
3. Verwijder de opmerkingen in Hallo-code in Hallo CheckCallerId methode. Deze methode wordt aangeroepen bij Hallo begin van elke actiemethode in het Hallo-controller. 
   
        private static void CheckCallerId()
        {
            string currentCallerClientId = ClaimsPrincipal.Current.FindFirst("appid").Value;
            string currentCallerServicePrincipalId = ClaimsPrincipal.Current.FindFirst("http://schemas.microsoft.com/identity/claims/objectidentifier").Value;
            if (currentCallerClientId != trustedCallerClientId || currentCallerServicePrincipalId != trustedCallerServicePrincipalId)
            {
                throw new HttpResponseException(new HttpResponseMessage { StatusCode = HttpStatusCode.Unauthorized, ReasonPhrase = "hello appID or service principal ID is not hello expected value." });
            }
        }
4. Hallo ToDoListDataAPI project tooAzure App Service implementeren.
5. Ga in uw browser toohello AngularJS-front-end van web-app HTTPS-URL en klik in de Hallo-startpagina op Hallo **tooDo lijst** tabblad.
   
    Hallo toepassing werkt niet omdat aanroepen toohello back-end mislukken. nieuwe code Hallo werkelijke appid en objectidentifier wordt gecontroleerd, maar deze heeft nog geen Hallo juiste waarden toocheck ze tegen. Hallo-browser de Console hulpprogramma's voor ontwikkelaars rapporten dat die Hallo-server retourneert een 401 HTTP-fout.
   
    ![Fout in Developer Tools Console](./media/app-service-api-dotnet-service-principal-auth/webapperror.png)
   
    In de stappen te volgen Hallo configureert u Hallo verwachte waarden.
6. Met Azure AD PowerShell, Hallo waarde ophalen van Hallo service principal voor hello Azure AD-toepassing die u hebt gemaakt voor Hallo TodoListWebApp project.
   
    a. Voor instructies over het tooinstall Azure PowerShell en verbinding maken met abonnement tooyour, Zie [Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md).
   
    b. een lijst met de service-principals tooget uitvoeren Hallo `Login-AzureRmAccount` opdracht in en klik vervolgens Hallo `Get-AzureRmADServicePrincipal` opdracht.
   
    c. Hallo objectid voor Hallo service-principal van Hallo TodoListAPI toepassing vinden en opslaan in een locatie die u later kunt kopiëren uit.
7. Navigeer in hello Azure-portal, toohello-blade API-app voor Hallo API-app die u hebt geïmplementeerd Hallo ToDoListDataAPI-project.
8. Klik op **instellingen > Toepassingsinstellingen**.
9. In Hallo **appinstellingen** sectie, Hallo volgende sleutels en waarden toevoegen:
   
   | **Sleutel** | TODO:TrustedCallerServicePrincipalId |
   | --- | --- |
   | **Waarde** |Service-principal-id van het aanroepen van toepassing |
   | **Voorbeeld** |4f4a94a4-6f0d-4072-4f4a94a4-6f0d-4072 |
   
   | **Sleutel** | TODO:TrustedCallerClientId |
   | --- | --- |
   | **Waarde** |Client-ID van het aanroepen van de toepassing - gekopieerd vanuit Hallo TodoListAPI Azure AD-toepassing |
   | **Voorbeeld** |960adec2-b74a-484a-960adec2-b74a-484a |
10. Klik op **Opslaan**.
    
     ![Op Opslaan klikken](./media/app-service-api-dotnet-service-principal-auth/trustedcaller.png)
11. In uw browser terug toohello van web-app-URL en in de startpagina Hallo op Hallo **tooDo lijst** tabblad.
    
     Deze toepassing hello werkt zoals verwacht omdat Hallo aanroeper vertrouwde app-ID en service-principal-ID Hallo verwachte waarden.
    
     ![pagina van de lijst met tooDo](./media/app-service-api-dotnet-service-principal-auth/mvchome.png)

## <a name="building-hello-projects-from-scratch"></a>Hallo-projecten helemaal bouwen
Hallo twee Web API-projecten zijn gemaakt met behulp van Hallo **Azure API-App** sjabloon en vervang Hallo standaard waarden domeincontroller met een domeincontroller ToDoList project. Voor het verkrijgen van Azure AD-service-principal tokens in de project ToDoListAPI Hallo Hallo [Active Directory Authentication Library (ADAL) voor .NET](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) NuGet-pakket is geïnstalleerd.

Zie voor een single-page application ' AngularJS informatie over het te maken met een Web-API-back-end zoals ToDoListAngular, [handen op Lab: bouwen van een enkele toepassing pagina WACHTWOORDVERIFICATIE met ASP.NET Web API en Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Voor informatie over het tooadd verificatiecode van Azure AD, Zie [beveiligen AngularJS één pagina Apps met Azure AD](../active-directory/active-directory-devquickstarts-angular.md).

## <a name="troubleshooting"></a>Problemen oplossen
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Zorg ervoor dat u en niet door elkaar ToDoListAPI (middelste laag) ToDoListDataAPI (gegevenslaag). Bijvoorbeeld: in deze zelfstudie u verificatie toohello gegevens laag API-app toevoegen **maar Hallo app-sleutel moet afkomstig zijn van Azure AD-toepassing die u hebt gemaakt voor de middelste laag API-app Hallo Hallo**.

## <a name="next-steps"></a>Volgende stappen
Dit is de laatste zelfstudie Hallo in Hallo reeks API-Apps. 

Zie voor meer informatie over Azure Active Directory Hallo resources te volgen.

* [Azure AD ontwikkelaarshandleiding](http://aka.ms/aaddev)
* [Azure AD-scenario 's](http://aka.ms/aadscenarios)
* [Azure AD-voorbeelden](http://aka.ms/aadsamples)
  
    Hallo [WebApp-WebAPI-OAuth2-AppIdentity-DotNet](http://github.com/AzureADSamples/WebApp-WebAPI-OAuth2-AppIdentity-DotNet) voorbeeld lijkt toowhat wordt weergegeven in deze zelfstudie, maar zonder verificatie van App Service.

Voor informatie over andere manieren toodeploy Visual Studio-projecten tooAPI-apps met behulp van Visual Studio of [implementatie automatiseren](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery) van een [broncodebeheersysteem](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control), Zie [hoe toodeploy een Azure App Service-app](../app-service-web/web-sites-deploy.md).


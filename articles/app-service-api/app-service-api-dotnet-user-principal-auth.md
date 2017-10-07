---
title: aaaUser verificatie voor API-Apps in Azure App Service | Microsoft Docs
description: Meer informatie over hoe een API-app in Azure App Service doordat tooprotect toegang krijgen tot enige tooauthenticated gebruikers.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 3896760d-46ff-4b67-b98a-edd233f24758
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: alkarche
ms.openlocfilehash: 4702fc77fcfe736405e22b033c35d22ae3c5a300
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Gebruikersverificatie voor API-Apps in Azure App Service
## <a name="overview"></a>Overzicht
Dit artikel laat zien hoe tooprotect een Azure-API-app zodat die alleen gebruikers geverifieerde deze kan aanroepen. Hallo artikel wordt ervan uitgegaan dat u Hallo hebt gelezen [overzicht van Azure App Service-authenticatie](../app-service/app-service-authentication-overview.md).

U leert het volgende:

* Hoe tooconfigure een verificatieprovider, met details voor Azure Active Directory (Azure AD).
* Hoe een API-app met behulp van beveiligde tooconsume Hallo [Active Directory Authentication Library (ADAL) voor JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).

Hallo artikel bestaat uit twee gedeelten:

* Hallo [hoe tooconfigure gebruikersverificatie in Azure App Service](#authconfig) sectie wordt uitgelegd hoe u algemene tooconfigure gebruikersverificatie voor API Apps en evenveel van toepassing is tooall frameworks die worden ondersteund door App Service, waaronder .NET, Node.js en Java.
* Beginnen met Hallo [u doorgaat met de .NET API Apps-zelfstudies Hallo](#tutorialstart) sectie, Hallo artikel handleidingen u bij het configureren van een voorbeeldtoepassing met .NET back-end en een AngularJS-front-end dat gebruikmaakt van Azure Active Directory voor gebruiker -verificatie. 

## <a id="authconfig"></a>Hoe tooconfigure gebruikersverificatie in Azure App Service
Deze sectie bevat algemene instructies die van toepassing zijn tooany API-app. Ga te voor stappen specifieke toohello tooDo lijst .NET-voorbeeldtoepassing[u doorgaat zelfstudies .NET-aan de slag Hallo](#tutorialstart).

1. In Hallo [Azure-portal](https://portal.azure.com/), navigeer toohello **instellingen** blade van Hallo API-app die u tooprotect, zoeken Hallo wilt **functies** sectie en klik vervolgens op  **Verificatie / autorisatie**.
   
    ![Azure-portal-verificatie/autorisatie](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. In Hallo **verificatie / autorisatie** blade, klikt u op **op**.
3. Selecteer een van de opties voor Hallo op Hallo **tootake actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst.
   
   * Als u wilt dat alleen geverifieerde aanroepen tooreach uw API-app, kiest u een Hallo **Meld u aan met...**  opties. Deze optie kunt u tooprotect Hallo API-app zonder het schrijven van code die in deze wordt uitgevoerd.
   * Als u wilt dat alle aanroepen tooreach uw API-app, kiest u **aanvraag toestaan (geen actie)**. U kunt deze optie niet-geverifieerde toodirect aanroepfuncties tooa keuze van verificatieproviders gebruiken. Met deze optie hebt u toowrite code toohandle autorisatie.
     
     Zie [Verificatie en autorisatie voor API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options) voor meer informatie.
4. Selecteer een of meer Hallo **verificatieproviders**.
   
    Hallo-afbeelding ziet u keuzes waarbij alle aanroepfuncties toobe geverifieerd door Azure AD.
   
    ![Azure-verificatie/autorisatie-portalblade](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    Wanneer u een verificatieprovider kiest, wordt in Hallo portal wordt een blade configuratie weergegeven voor die provider. 
   
    Zie voor gedetailleerde instructies waarin wordt uitgelegd hoe tooconfigure verificatie provider configuratie blades Hallo [hoe tooconfigure uw App Service-toepassing toouse Azure Active Directory-aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (Hallo koppeling gaat tooan artikel over Azure AD, maar Hallo artikel zelf bevat tabbladen die een koppeling tooarticles voor Hallo andere verificatieproviders.)
5. Wanneer u met de Hallo verificatie provider configuratie blade bent klaar, klikt u op **OK**.
6. In Hallo **verificatie / autorisatie** blade, klikt u op **opslaan**.

Wanneer dit wordt gedaan, wordt alle API-aanroepen in App Service geverifieerd voordat ze Hallo API-app bereiken. Hallo-verificatie werken Hallo gelijk voor alle talen die App-service wordt ondersteund, waaronder .NET, Node.js en Java. 

toomake geverifieerd API-aanroepen, Hallo aanroeper bevat Hallo-verificatieprovider OAuth 2.0-bearer-token in autorisatie-header Hallo van HTTP-aanvragen. Hallo-token kan worden verkregen met behulp van de SDK Hallo-verificatieprovider.

## <a id="tutorialstart"></a>U kunt doorgaan Hallo .NET API Apps-zelfstudies
Als u Hallo Node.js of Java-zelfstudies voor API-apps volgt, slaat u het volgende artikel toohello, [principal verificatie van de service voor API-apps](app-service-api-dotnet-service-principal-auth.md). 

Als u Hallo .NET-zelfstudie serie voor API-apps volgt en al Hallo voorbeeldtoepassing hebben geïmplementeerd zoals beschreven in Hallo [eerste](app-service-api-dotnet-get-started.md) en [tweede](app-service-api-cors-consume-javascript.md) zelfstudies overslaan toohello [instellen verificatie in App Service en Azure AD](#azureauth) sectie.

Als u deze zelfstudie toofollow wilt zonder tussenkomst van de eerste en tweede zelfstudies hello, Hallo volgende stappen uit die wordt uitgelegd hoe tooget gestart met behulp van een geautomatiseerd proces toodeploy Hallo-voorbeeldtoepassing.

> [!NOTE]
> Hallo volgende stappen kunnen u dezelfde uitgangspunt als wanneer u de eerste twee zelfstudies, met één uitzondering Hallo toohello: Visual Studio al weet niet welk web-app of API-app die elk project wordt geïmplementeerd. Dit betekent dat u hebt geen exacte instructies in deze zelfstudie waarin wordt uitgelegd hoe toodeploy toohello rechts doelen. Als u niet vertrouwd bent met uitzoeken hoe toodo Hallo zelf implementatiestappen, is het beter toofollow Hallo zelfstudie reeks van Hallo [eerste zelfstudie](app-service-api-dotnet-get-started.md) dan toostart met deze automatische implementatie.
> 
> 

1. Zorg ervoor dat u beschikt over alle Hallo vereisten in Hallo [eerste zelfstudie](app-service-api-dotnet-get-started.md). Deze zelfstudies verificatie in toevoeging toohello vereisten die worden vermeld, wordt ervan uitgegaan dat u eerder hebt gewerkt met App Service-web-apps en API-apps in Visual Studio en hello Azure-portal.
2. Klik op Hallo **tooAzure implementeren** knop in Hallo [tooDo lijst opslagplaats Leesmij-voorbeeldbestand](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) toodeploy Hallo API apps en Hallo web-app. Noteer hello Azure-resourcegroep die wordt gemaakt, zoals u dit later toolook van web-app en API-app-namen kunt.
3. Download of kloon Hallo [tooDo lijst voorbeeld opslagplaats](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) tooget Hallo code die u met lokaal in Visual Studio werkt.

## <a id="azureauth"></a>Verificatie in App Service en Azure AD instellen
U hebt nu Hallo toepassing die wordt uitgevoerd in Azure App Service zonder dat gebruikers worden geverifieerd. In deze sectie kunt u verificatie toevoegt als volgt Hallo taken te volgen:

* Verificatie van App Service toorequire Azure Active Directory (Azure AD) voor het aanroepen van Hallo middelste laag API-app configureren.
* Maak een Azure AD-toepassing.
* Configureer hello Azure AD-toepassing toosend hello bearer-token na aanmelding toohello AngularJS-front-end. 

Als u problemen bij de volgende zelfstudie Hallo-instructies, Zie Hallo [probleemoplossing](#troubleshooting) sectie aan einde van de zelfstudie Hallo Hallo. 

### <a name="configure-authentication-for-hello-middle-tier-api-app"></a>Verificatie voor de middelste laag Hallo API-app configureren
1. In Hallo [Azure-portal](https://portal.azure.com/), navigeer toohello **instellingen** blade van Hallo API-app die u hebt gemaakt voor het project ToDoListAPI Hallo Hallo zoeken **functies** sectie, en vervolgens Klik op **verificatie / autorisatie**.
   
    ![Azure-portal-verificatie/autorisatie](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. In Hallo **verificatie / autorisatie** blade, klikt u op **op**.
3. In Hallo **tootake actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst, selecteer **aanmelden met Azure Active Directory**.
   
    Deze optie zorgt ervoor dat er geen aanvragen voor unauathenticated Hallo API-app wordt bereiken. 
4. Onder **verificatieproviders**, klikt u op **Azure Active Directory**.
   
    ![Azure-verificatie/autorisatie-portalblade](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. In Hallo **Azure Active Directory-instellingen** blade, klikt u op **Express**
   
    ![Azure portal-verificatie/autorisatie Express optie](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    Hello **Express** optie App Service kunt automatisch een Azure AD-toepassing maken in uw Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    U hebt geen toocreate een tenant, omdat elke Azure-account automatisch een heeft.
6. Onder **beheermodus**, klikt u op **nieuwe AD-App maken** als deze niet al is geselecteerd en Let op Hallo-waarde die in Hallo **App maken** tekstvak; u moet deze AAD opzoeken de toepassing in de klassieke Azure-portal later Hallo.
   
    ![Azure-portal Azure AD-instellingen](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure maakt automatisch een Azure AD-toepassing met de opgegeven naam Hallo in uw Azure AD-tenant. Naam standaard hello Azure AD-toepassing hello dezelfde als Hallo API-app. Als u liever, kunt u een andere naam.
7. Klik op **OK**.
8. In Hallo **verificatie / autorisatie** blade, klikt u op **opslaan**.
   
    ![Op Opslaan klikken](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Alleen gebruikers in uw Azure AD-tenant kunnen nu Hallo API-app aanroepen.

### <a name="optional-test-hello-api-app"></a>Optioneel: Hallo API app testen
1. Ga in een browser toohello-URL van Hallo API-app: in Hallo **API-app** blade in hello Azure-portal, klikt u op de koppeling onder Hallo **URL**.  
   
    U bent omgeleide tooa aanmeldingsscherm omdat niet-geverifieerde aanvragen tooreach Hallo API-app niet zijn toegestaan.
   
    Als uw browser toohello 'is gemaakt' pagina gaat, Hallo browser al kan worden geregistreerd op--in dat geval open een InPrivate- of Incognito-venster en ga toohello API-app-URL.
2. Meld u aan met referenties voor een gebruiker in uw Azure AD-tenant.
   
    Wanneer u bent aangemeld, wordt de pagina 'gemaakt' hello weergegeven in Hallo browser.
3. De browser sluiten Hallo.

### <a name="configure-hello-azure-ad-application"></a>De toepassing hello Azure AD configureren
Wanneer u Azure AD-verificatie hebt geconfigureerd, wordt in App Service een Azure AD-toepassing voor u gemaakt. Hallo nieuwe Azure AD-toepassing is standaard geconfigureerd tooprovide hello bearer-token toohello van API-app-URL. In deze sectie configureert u hello Azure AD toepassing tooprovide hello bearer-token toohello AngularJS-front-end in plaats van rechtstreeks toohello middelste laag API-app. Hallo AngularJS-front-end stuurt Hallo token toohello API-app wanneer deze API-app Hallo aanroept.

> [!NOTE]
> tookeep hello proces zo eenvoudig mogelijk, voor deze zelfstudie wordt een enkele Azure AD gebruikt een toepassing voor zowel Hallo-front-end en Hallo middelste laag API-app. Een andere optie is toouse twee Azure AD-toepassingen. In dat geval hebt u toogive Hallo-front-end van Azure AD-toepassing machtiging toocall Hallo middelste laag van Azure AD-toepassing. Deze aanpak meerdere toepassingen, krijgt u meer gedetailleerde controle over machtigingen tooeach laag.
> 
> 

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), gaat u te**Azure Active Directory**.
   
   U hebt toouse Hallo klassieke portal omdat bepaalde Azure Active Directory-instellingen die u moet toegang hebben tot tooare nog niet beschikbaar in Hallo huidige Azure-portal.
2. Op Hallo **Directory** tabblad, klikt u op uw AAD-tenant.
   
   ![Azure AD in de klassieke portal](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Klik op **toepassingen > Mijn bedrijf eigenaar is van toepassingen**, en klik vervolgens op het vinkje Hallo.
   
   Mogelijk hebt u ook toorefresh Hallo pagina toosee Hallo nieuwe toepassing.
4. Klik op Hallo naam Hallo die Azure voor u gemaakt wanneer u verificatie is ingeschakeld voor uw API-app in de lijst met toepassingen Hallo.
   
   ![Op het tabblad Azure AD-toepassingen](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. Klik op **Configureren**
   
   ![Tabblad met Azure AD configureren](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Stel **aanmeldings-URL** toohello-URL voor uw AngularJS-web-app, geen afsluitende slash.
   
   Bijvoorbeeld: https://todolistangular.azurewebsites.net
   
   ![Aanmeldings-URL](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Stel **antwoord-URL** toohello-URL voor uw web-app geen afsluitende slash.
   
   Bijvoorbeeld: https://todolistsangular.azurewebsites.net
8. Klik op **Opslaan**.
   
   ![Antwoord-URL](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. Aan de onderkant van de Hallo van Hallo pagina, klikt u op **beheren manifest > downloaden manifest**.
   
   ![Downloaden van het manifest](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Download Hallo tooa bestandslocatie waar u het kunt bewerken.
11. Zoek in Hallo gedownload van een manifestbestand op Hallo `oauth2AllowImplicitFlow` eigenschap. Hallo-waarde van deze eigenschap van wijzigen `false` te`true`, en sla Hallo-bestand.
    
    Deze instelling is vereist voor toegang tot een JavaScript-toepassing voor één pagina. Hiermee kunt Hallo Oauth 2.0 bearer-token toobe in Hallo URL-fragment geretourneerd.
12. Klik op **beheren manifest > uploaden manifest**, en het uploaden van Hallo-bestand dat u in de voorgaande stap Hallo bijgewerkt.
    
    ![Uploaden van het manifest](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Kopiëren Hallo **Client-ID** waarde en sla dit op een locatie kunt u dit uit later downloaden.

## <a name="configure-hello-todolistangular-project-toouse-authentication"></a>Hallo ToDoListAngular project toouse verificatie configureren
In deze sectie wijzigen Hallo AngularJS-front-end dat gebruikmaakt van Active Directory Authentication Library (ADAL) voor JS tooacquire bearer-token voor Hallo aangemelde gebruiker van Azure AD. Hallo code neemt Hallo-token in HTTP-aanvragen verzonden toohello middelste laag, zoals wordt weergegeven in het volgende diagram Hallo. 

![Gebruiker-verificatiediagram](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

Controleer Hallo toofiles wijzigingen in de project ToDoListAngular hello te volgen.

1. Open Hallo *index.cshtml* bestand.
2. Verwijder de opmerkingen in Hallo-regels die verwijzen naar Hallo Active Directory Authentication Library (ADAL) voor JS scripts.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Open Hallo *app/scripts/app.js* bestand.
4. Hallo codeblok commentaar gemarkeerd voor 'zonder verificatie' en verwijder het commentaarteken Hallo codeblok gemarkeerd voor 'met verificatie'.
   
    Deze wijziging verwijst naar Hallo ADAL JS verificatieprovider en configuratie waarden tooit biedt. In Hallo stappen stelt u Hallo configuratiewaarden voor uw API-app en Azure AD-toepassing.
5. Hallo-code die wordt ingesteld Hallo `endpoints` variabele, stel Hallo API URL toohello URL van Hallo API-app die u hebt gemaakt voor ToDoListAPI-project Hallo en stel hello Azure AD-toepassing-ID toohello client-ID die u hebt gekopieerd uit Hallo klassieke Azure-portal.
   
    Hallo-code is nu vergelijkbare toohello voorbeeld te volgen.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. In Hallo roept te`adalProvider.init`stelt `tenant` tooyour tenantnaam en `clientId` toosame-waarde die u in de vorige stap Hallo gebruikt.
   
    Hallo-code is nu vergelijkbare toohello voorbeeld te volgen.
   
        adalProvider.init(
            {
                instance: 'https://login.microsoftonline.com/', 
                tenant: 'contoso.onmicrosoft.com',
                clientId: '1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3',
                extraQueryParameter: 'nux=1',
                endpoints: endpoints
            },
            $httpProvider
            );
   
    Deze wijzigingen te`app.js` opgeven dat de aanroepende code Hallo en Hallo API aangeroepen in Hallo dezelfde Azure AD-toepassing zijn.
7. Open Hallo *app/scripts/homeCtrl.js* bestand.
8. Hallo codeblok commentaar gemarkeerd voor 'zonder verificatie' en verwijder het commentaarteken Hallo codeblok gemarkeerd voor 'met verificatie'.
9. Open Hallo *app/scripts/indexCtrl.js* bestand.
10. Hallo codeblok commentaar gemarkeerd voor 'zonder verificatie' en verwijder het commentaarteken Hallo codeblok gemarkeerd voor 'met verificatie'.

### <a name="deploy-hello-todolistangular-project-tooazure"></a>Hallo ToDoListAngular project tooAzure implementeren
1. In **Solution Explorer**, met de rechtermuisknop op Hallo ToDoListAngular project en klik vervolgens op **publiceren**.
2. Klik op **Publish**.
   
    Visual Studio implementeert Hallo-project en basis-URL in een browser toohello van web-app wordt geopend. Hier ziet een fout 403-pagina normaal voor een poging toogo tooa Web API basis-URL vanuit een browser is.
   
    U hebt nog toomake wijziging toohello middelste laag API-app voordat u de toepassing hello kunt testen.
3. De browser sluiten Hallo.

## <a name="configure-hello-todolistapi-project-toouse-authentication"></a>Hallo ToDoListAPI-project toouse verificatie configureren
ToDoListAPI-project verzendt momenteel Hallo ' * ' als Hallo `owner` tooToDoListDataAPI waarde. In deze sectie kunt u Hallo code toosend Hallo-ID van Hallo aangemelde gebruiker wijzigen.

Hallo volgende wijzigingen in Hallo ToDoListAPI-project maken

1. Open Hallo *Controllers/ToDoListController.cs* bestand en het commentaar verwijderen Hallo regel in elke actiemethode voor de die wordt ingesteld `owner` toohello Azure AD `NameIdentifier` claimwaarde. Bijvoorbeeld:
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Belangrijke**: Verwijder de code in Hallo geen opmerkingen `ToDoListDataAPI` methode; doet u dat later voor Hallo-zelfstudie voor verificatie.

### <a name="deploy-hello-todolistapi-project-tooazure"></a>Hallo ToDoListAPI-project tooAzure implementeren
1. In **Solution Explorer**, met de rechtermuisknop op Hallo ToDoListAPI-project en klik vervolgens op **publiceren**.
2. Klik op **Publish**.
   
    Visual Studio implementeert Hallo-project en basis-URL in een browser toohello van API-app wordt geopend.
3. De browser sluiten Hallo.

### <a name="test-hello-application"></a>Hallo toepassing testen
1. Ga toohello-URL van de web-app hello, **met behulp van HTTPS niet HTTP**.
2. Klik op Hallo **tooDo lijst** tabblad.
   
    U bent na vragen aan gebruiker toolog in.
3. Aanmelden met referenties op Hallo van een gebruiker in uw AAD-tenant.
4. Hallo **tooDo lijst** pagina wordt weergegeven.
   
   ![pagina van de lijst met tooDo](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   Er is geen taakitems worden weergegeven omdat tot op heden alle eigenaar zijn ' * '. Nu de middelste laag Hallo-items voor Hallo aangemelde gebruiker vraagt en geen nog zijn gemaakt.
5. Toevoegen van nieuwe taak items tooverify die toepassing hello werkt.
6. Ga in een ander browservenster toohello Swagger-gebruikersinterface-URL voor Hallo ToDoListDataAPI API-app en klik op **ToDoList > ophalen**. Geef een sterretje voor Hallo `owner` parameter en klik vervolgens op **Try it out in**.
   
   antwoord Hallo ziet u dat nieuwe taakitems Hallo Hallo werkelijke Azure AD-gebruikers-ID in de eigenschap Owner Hallo hebben.
   
   ![Eigenaar-ID in JSON-antwoord](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-hello-projects-from-scratch"></a>Hallo-projecten helemaal bouwen
Hallo twee Web API-projecten zijn gemaakt met behulp van Hallo **Azure API-App** sjabloon en vervang Hallo standaard waarden domeincontroller met een domeincontroller ToDoList project. 

Zie voor een single-page application ' AngularJS informatie over het te maken met een Web API 2 back-end, [handen op Lab: bouwen van een enkele toepassing pagina WACHTWOORDVERIFICATIE met ASP.NET Web API en Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Voor informatie over het tooadd verificatiecode van Azure AD, Zie Hallo resources te volgen:

* [Apps met Azure AD beveiligen AngularJS één pagina](../active-directory/active-directory-devquickstarts-angular.md).
* [Introductie van ADAL JS v1](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Problemen oplossen
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Zorg ervoor dat u en niet door elkaar ToDoListAPI (middelste laag) ToDoListDataAPI (gegevenslaag). Controleer bijvoorbeeld of u verificatie toohello middelste laag API-app, niet de gegevenslaag Hallo toegevoegd. 
* Zorg ervoor dat Hallo AngularJS source code verwijzingen Hallo middelste laag API app-URL (ToDoListAPI, niet ToDoListDataAPI) en Hallo Azure AD-client-ID juist. 

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toouse App Service-verificatie voor een API-app en hoe toocall API-app met behulp van Hallo Hallo ADAL JS library. In de volgende zelfstudie Hallo leert u hoe te[veilige toegang tooyour API-app voor scenario's voor service to service](app-service-api-dotnet-service-principal-auth.md).


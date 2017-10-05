---
title: Gebruikersverificatie voor API-Apps in Azure App Service | Microsoft Docs
description: Informatie over het beveiligen van een API-app in Azure App Service doordat alleen toegang tot geverifieerde gebruikers.
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
ms.openlocfilehash: a5b713f3a60b3886d813438496d704f464d914e6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="user-authentication-for-api-apps-in-azure-app-service"></a>Gebruikersverificatie voor API-Apps in Azure App Service
## <a name="overview"></a>Overzicht
In dit artikel laat zien hoe een Azure-API-app beveiligen zodat alleen geverifieerde gebruikers kunnen worden aanroepen. Het artikel wordt ervan uitgegaan dat u hebt gelezen de [overzicht van Azure App Service-authenticatie](../app-service/app-service-authentication-overview.md).

U leert het volgende:

* Klik hier voor meer informatie over het configureren van een verificatieprovider, met details voor Azure Active Directory (Azure AD).
* Een beveiligde API-app gebruiken met behulp van de [Active Directory Authentication Library (ADAL) voor JavaScript](https://github.com/AzureAD/azure-activedirectory-library-for-js).

Het artikel bestaat uit twee gedeelten:

* De [gebruikersverificatie configureren in Azure App Service](#authconfig) .NET, Node.js, met inbegrip van sectie wordt uitgelegd in het algemeen het configureren van gebruikersverificatie voor API Apps en is evenveel van toepassing op alle frameworks die worden ondersteund door App Service en Java.
* Beginnen met de [u doorgaat met de .NET API Apps-zelfstudies](#tutorialstart) sectie, het artikel begeleidt u bij het configureren van een voorbeeldtoepassing met een .NET-back-end en een AngularJS-front-end dat gebruikmaakt van Azure Active Directory voor gebruiker -verificatie. 

## <a id="authconfig"></a>Verificatie van de gebruiker in Azure App Service configureren
Deze sectie bevat algemene instructies die betrekking hebben op elke API-app. Voor specifieke stappen voor de voorbeeldtoepassing te doen lijst-.NET, gaat u naar [u doorgaat met de zelfstudies .NET aan de slag](#tutorialstart).

1. In de [Azure-portal](https://portal.azure.com/), gaat u naar de **instellingen** blade van de API-app die u wilt beveiligen, vinden de **functies** sectie en klik vervolgens op  **Verificatie / autorisatie**.
   
    ![Azure-portal-verificatie/autorisatie](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. In de **verificatie / autorisatie** blade, klikt u op **op**.
3. Selecteer een van de opties uit de **te ondernemen actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst.
   
   * Als u wilt dat alleen geverifieerde aanroepen naar uw API-app te bereiken, kies een van de **Meld u aan met...**  opties. Deze optie kunt u de API-app beveiligen zonder het schrijven van code die in deze wordt uitgevoerd.
   * Als u wilt dat alle aanroepen voor het bereiken van uw API-app, kiest u **aanvraag toestaan (geen actie)**. U kunt deze optie gebruiken om niet-geverifieerde aanroepfuncties een keuze uit verificatieproviders leiden. Met deze optie hebt u code schrijven om de verwerking van autorisatie.
     
     Zie [Verificatie en autorisatie voor API Apps in Azure App Service](app-service-api-authentication.md#multiple-protection-options) voor meer informatie.
4. Selecteer een of meer van de **verificatieproviders**.
   
    De afbeelding toont keuzes waarbij alle aanroepfuncties moet worden geverifieerd door Azure AD.
   
    ![Azure-verificatie/autorisatie-portalblade](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
   
    Als u een verificatieprovider kiest, de portal wordt weergegeven van een configuratie-blade voor die provider. 
   
    Zie voor gedetailleerde instructies met uitleg over het configureren van de verificatie-provider configuratie blades [het configureren van uw App Service-toepassing voor het gebruik van Azure Active Directory-aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). (De koppeling gaat u naar een artikel over Azure AD, maar het artikel zelf bevat tabbladen die een koppeling naar artikelen voor de authenticatieproviders.)
5. Wanneer u met de blade verificatie provider configuratie bent klaar, klikt u op **OK**.
6. In de **verificatie / autorisatie** blade, klikt u op **opslaan**.

Wanneer dit wordt gedaan, wordt alle API-aanroepen in App Service geverifieerd voordat ze de API-app bereiken. De verificatieservices werkt hetzelfde voor alle talen die App-service wordt ondersteund, waaronder .NET, Node.js en Java. 

Als u geverifieerde API-aanroepen, bevat de aanroeper de verificatieprovider OAuth 2.0-bearer-token in autorisatie-header van HTTP-aanvragen. Het token kan worden verkregen met behulp van de verificatieprovider SDK.

## <a id="tutorialstart"></a>U kunt doorgaan de zelfstudies .NET API-Apps
Als u de zelfstudies Node.js of Java voor API-apps volgt, gaat u naar het volgende artikel [principal verificatie van de service voor API-apps](app-service-api-dotnet-service-principal-auth.md). 

Als u de .NET-zelfstudie-reeks voor API-apps volgt en al de voorbeeldtoepassing hebben geïmplementeerd zoals beschreven in de [eerste](app-service-api-dotnet-get-started.md) en [tweede](app-service-api-cors-consume-javascript.md) zelfstudies, gaat u verder met de [instellen verificatie in App Service en Azure AD](#azureauth) sectie.

Als u Volg deze zelfstudie wilt zonder tussenkomst van de eerste en tweede zelfstudies, doet u de volgende stappen die wordt uitgelegd hoe u aan de slag met behulp van een geautomatiseerd proces voor het implementeren van de voorbeeldtoepassing.

> [!NOTE]
> De volgende stappen kunnen u naar het hetzelfde beginpunt als wanneer u de eerste twee zelfstudies, met één uitzondering is: Visual Studio al weet niet welk web-app of API-app die elk project wordt geïmplementeerd. Dit betekent dat u hebt geen exacte instructies in deze zelfstudie waarin wordt uitgelegd hoe om te implementeren op de juiste doelen. Als u niet vertrouwd bent met hoe de implementatiestappen zelf doen, is het beter te volgen van de zelfstudie reeks van de [eerste zelfstudie](app-service-api-dotnet-get-started.md) dan beginnen met dit implementatieproces geautomatiseerd.
> 
> 

1. Zorg dat u alle vereisten die worden vermeld in de [eerste zelfstudie](app-service-api-dotnet-get-started.md). Naast de vereisten die worden vermeld, deze zelfstudies verificatie wordt ervan uitgegaan dat u hebt gewerkt met App Service-web-apps en API-apps in Visual Studio en de Azure-portal.
2. Klik op de **implementeren in Azure** knop in de [To Do List voorbeeld opslagplaats Leesmij-bestand](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/readme.md) om de API-apps en de web-app te implementeren. Noteer de Azure-resourcegroep die wordt gemaakt, zoals u dit kunt later om web-app en de namen van de API-app te zoeken.
3. Downloaden of te klonen de [To Do List voorbeeld opslagplaats](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) ophalen van de code die u met lokaal in Visual Studio werkt.

## <a id="azureauth"></a>Verificatie in App Service en Azure AD instellen
U hebt nu de toepassing die wordt uitgevoerd in Azure App Service zonder dat gebruikers worden geverifieerd. In deze sectie kunt u verificatie toevoegt als volgt u de volgende taken:

* App Service configureren voor Azure Active Directory (Azure AD) verificatie vereisen voor het aanroepen van de middelste laag API-app.
* Maak een Azure AD-toepassing.
* De Azure AD-toepassing de bearer-token na aanmelding verzenden naar de AngularJS-front-end configureren. 

Als u problemen ondervindt tijdens de zelfstudie aanwijzingen, raadpleegt u de [probleemoplossing](#troubleshooting) sectie aan het einde van de zelfstudie. 

### <a name="configure-authentication-for-the-middle-tier-api-app"></a>Verificatie voor de middelste laag API-app configureren
1. In de [Azure-portal](https://portal.azure.com/), gaat u naar de **instellingen** blade van de API-app die u hebt gemaakt voor het project ToDoListAPI, vinden de **functies** sectie en klik vervolgens op  **Verificatie / autorisatie**.
   
    ![Azure-portal-verificatie/autorisatie](./media/app-service-api-dotnet-user-principal-auth/features.png)
2. In de **verificatie / autorisatie** blade, klikt u op **op**.
3. In de **te ondernemen actie wanneer de aanvraag is niet geverifieerd** vervolgkeuzelijst, selecteer **aanmelden met Azure Active Directory**.
   
    Deze optie zorgt ervoor dat er geen aanvragen voor unauathenticated wordt toegang heeft tot de API-app. 
4. Onder **verificatieproviders**, klikt u op **Azure Active Directory**.
   
    ![Azure-verificatie/autorisatie-portalblade](./media/app-service-api-dotnet-user-principal-auth/authblade.png)
5. In de **Azure Active Directory-instellingen** blade, klikt u op **Express**
   
    ![Azure portal-verificatie/autorisatie Express optie](./media/app-service-api-dotnet-user-principal-auth/aadsettings.png)
   
    Met de **Express** optie App Service kunt automatisch een Azure AD-toepassing maken in uw Azure AD [tenant](https://msdn.microsoft.com/en-us/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant). 
   
    U hoeft te maken van een tenant omdat elke Azure-account automatisch een heeft.
6. Onder **beheermodus**, klikt u op **nieuwe AD-App maken** als deze niet al is geselecteerd en Let op de waarde die in de **App maken** tekstvak; u moet deze AAD opzoeken later toepassing in de klassieke Azure portal.
   
    ![Azure-portal Azure AD-instellingen](./media/app-service-api-dotnet-user-principal-auth/aadsettings2.png)
   
    Azure maakt automatisch een Azure AD-toepassing met de naam van de aangegeven in uw Azure AD-tenant. Standaard is de Azure AD-toepassing naam hetzelfde zijn als de API-app. Als u liever, kunt u een andere naam.
7. Klik op **OK**.
8. In de **verificatie / autorisatie** blade, klikt u op **opslaan**.
   
    ![Op Opslaan klikken](./media/app-service-api-dotnet-user-principal-auth/authsave.png)

Alleen gebruikers in uw Azure AD-tenant kunnen nu de API-app aanroepen.

### <a name="optional-test-the-api-app"></a>Optioneel: Het testen van de API-app
1. Ga in een browser naar de URL van de API-app: in de **API-app** blade in de Azure-portal klikt u op de koppeling onder **URL**.  
   
    U wordt omgeleid naar een aanmeldingsscherm omdat niet-geverifieerde aanvragen zijn niet toegestaan voor het bereiken van de API-app.
   
    Als uw browser gaat naar de pagina 'is gemaakt', kan al de browser worden geregistreerd op--in dat geval open een InPrivate- of Incognito-venster en Ga naar de API-app-URL.
2. Meld u aan met referenties voor een gebruiker in uw Azure AD-tenant.
   
    Wanneer u bent aangemeld, wordt de pagina 'is gemaakt' in de browser weergegeven.
3. Sluit de browser.

### <a name="configure-the-azure-ad-application"></a>De toepassing Azure AD configureren
Wanneer u Azure AD-verificatie hebt geconfigureerd, wordt in App Service een Azure AD-toepassing voor u gemaakt. Toepassing is standaard ingesteld op de nieuwe Azure AD geconfigureerd voor de bearer-token naar de API-app-URL. In deze sectie configureert u de Azure AD-toepassing voor de bearer-token naar de AngularJS front-end in plaats van rechtstreeks op de middelste laag API-app. De AngularJS-front-end stuurt het token naar de API-app wanneer de API-app roept.

> [!NOTE]
> Bewaren van het proces als eenvoudig mogelijk, deze zelfstudie maakt gebruik van een enkele Azure AD-toepassing voor zowel de front-end- en het midden gegevenslaag vormt API-app. Een andere optie is het gebruik van twee Azure AD-toepassingen. In dat geval moet u de front-end Azure AD-toepassing toestemming om aan te roepen Azure AD-toepassing voor de middelste laag geven. Deze aanpak meerdere toepassingen, krijgt u meer gedetailleerde controle over machtigingen voor elke laag.
> 
> 

1. In de [klassieke Azure-portal](https://manage.windowsazure.com/), gaat u naar **Azure Active Directory**.
   
   U moet de klassieke portal gebruiken, omdat bepaalde Azure Active Directory-instellingen die u toegang tot moet nog niet beschikbaar in de huidige Azure-portal zijn.
2. Op de **Directory** tabblad, klikt u op uw AAD-tenant.
   
   ![Azure AD in de klassieke portal](./media/app-service-api-dotnet-user-principal-auth/selecttenant.png)
3. Klik op **toepassingen > Mijn bedrijf eigenaar is van toepassingen**, en klik vervolgens op het vinkje.
   
   Mogelijk moet u ook Vernieuw de pagina overzicht van de nieuwe toepassing.
4. Klik in de lijst met toepassingen op de naam van de gebruiker die Azure voor u gemaakt wanneer u verificatie is ingeschakeld voor uw API-app.
   
   ![Op het tabblad Azure AD-toepassingen](./media/app-service-api-dotnet-user-principal-auth/appstab.png)
5. Klik op **Configureren**
   
   ![Tabblad met Azure AD configureren](./media/app-service-api-dotnet-user-principal-auth/configure.png)
6. Stel **aanmeldings-URL** op de URL voor uw AngularJS-web-app, geen afsluitende slash.
   
   Bijvoorbeeld: https://todolistangular.azurewebsites.net
   
   ![Aanmeldings-URL](./media/app-service-api-dotnet-user-principal-auth/signonurlazure.png)
7. Stel **antwoord-URL** op de URL voor uw web-app geen afsluitende slash.
   
   Bijvoorbeeld: https://todolistsangular.azurewebsites.net
8. Klik op **Opslaan**.
   
   ![Antwoord-URL](./media/app-service-api-dotnet-user-principal-auth/replyurlazure.png)
9. Klik onder aan de pagina op **beheren manifest > downloaden manifest**.
   
   ![Downloaden van het manifest](./media/app-service-api-dotnet-user-principal-auth/downloadmanifest.png)
10. Download het bestand naar een locatie waar u het kunt bewerken.
11. Zoek in het gedownloade manifestbestand voor het `oauth2AllowImplicitFlow` eigenschap. Wijzig de waarde van deze eigenschap van `false` naar `true`, en sla het bestand.
    
    Deze instelling is vereist voor toegang tot een JavaScript-toepassing voor één pagina. Kan de Oauth 2.0-bearer-token wordt in het URL-fragment geretourneerd.
12. Klik op **beheren manifest > uploaden manifest**, en upload het bestand dat u in de vorige stap hebt bijgewerkt.
    
    ![Uploaden van het manifest](./media/app-service-api-dotnet-user-principal-auth/uploadmanifest.png)
13. Kopieer de **Client-ID** waarde en sla dit op een locatie kunt u dit uit later downloaden.

## <a name="configure-the-todolistangular-project-to-use-authentication"></a>Configureren van het project ToDoListAngular om verificatie te gebruiken
In deze sectie wijzigt u de AngularJS-front-end dat gebruikmaakt van Active Directory Authentication Library (ADAL) voor JS te verkrijgen van een bearer-token voor de aangemelde gebruiker van Azure AD. De code neemt het token in HTTP-aanvragen verzonden naar de middelste laag, zoals wordt weergegeven in het volgende diagram. 

![Gebruiker-verificatiediagram](./media/app-service-api-dotnet-user-principal-auth/appdiagram.png)

De volgende wijzigingen aanbrengen in bestanden in het project ToDoListAngular.

1. Open de *index.cshtml* bestand.
2. Verwijder de opmerkingen in de regels die verwijzen naar de Active Directory Authentication Library (ADAL) voor JS scripts.
   
        <script src="app/scripts/adal.js"></script>
        <script src="app/scripts/adal-angular.js"></script>
3. Open de *app/scripts/app.js* bestand.
4. Het codeblok gemarkeerd voor 'zonder verificatie' uitcommentariëren en verwijder de opmerkingen in het codeblok gemarkeerd voor 'met verificatie'.
   
    Deze wijziging verwijst naar de ADAL JS verificatieprovider en biedt configuratiewaarden aan. In de volgende stappen stelt u de configuratiewaarden voor uw API-app en Azure AD-toepassing.
5. In de code die Hiermee stelt u de `endpoints` variabele, de API-URL naar de URL van de API-app instellen dat u voor het project ToDoListAPI gemaakt en de Azure AD-toepassings-ID ingesteld op de client-ID die u hebt gekopieerd uit de klassieke Azure portal.
   
    De code is nu vergelijkbaar met het volgende voorbeeld.
   
        var endpoints = {
            "https://todolistapi0121.azurewebsites.net/": "1cf55bc9-9ed8-4df31cf55bc9-9ed8-4df3"
        };
6. In de aanroep naar `adalProvider.init`stelt `tenant` aan de tenantnaam van uw en `clientId` op dezelfde waarde die u hebt gebruikt in de vorige stap.
   
    De code is nu vergelijkbaar met het volgende voorbeeld.
   
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
   
    Deze wijzigingen naar `app.js` opgeven dat de aanroepende code en de API aangeroepen zich in dezelfde Azure AD-toepassing.
7. Open de *app/scripts/homeCtrl.js* bestand.
8. Het codeblok gemarkeerd voor 'zonder verificatie' uitcommentariëren en verwijder de opmerkingen in het codeblok gemarkeerd voor 'met verificatie'.
9. Open de *app/scripts/indexCtrl.js* bestand.
10. Het codeblok gemarkeerd voor 'zonder verificatie' uitcommentariëren en verwijder de opmerkingen in het codeblok gemarkeerd voor 'met verificatie'.

### <a name="deploy-the-todolistangular-project-to-azure"></a>Het project ToDoListAngular implementeren in Azure
1. Klik in **Solution Explorer** met de rechtermuisknop op het project ToDoListAngular. Klik vervolgens op **Publish**.
2. Klik op **Publish**.
   
    Visual Studio implementeert het project en opent een browservenster met de basis-URL van de web-app. Hier ziet een fout 403-pagina normaal voor een poging is om naar een Web-API basis-URL vanuit een browser.
   
    U hebt nog wel een wijziging aanbrengt in de middelste laag API-app voordat u kunt de toepassing testen.
3. Sluit de browser.

## <a name="configure-the-todolistapi-project-to-use-authentication"></a>Configureren van het project ToDoListAPI om verificatie te gebruiken
Op dit moment het project ToDoListAPI verzendt ' * ' als de `owner` waarde ToDoListDataAPI. In deze sectie kunt u de code voor het verzenden van de ID van de aangemelde gebruiker wijzigen.

De volgende wijzigingen aanbrengen in het project ToDoListAPI.

1. Open de *Controllers/ToDoListController.cs* bestand en het commentaar verwijderen van de regel in elke actiemethode voor de die wordt ingesteld `owner` met Azure AD `NameIdentifier` claimwaarde. Bijvoorbeeld:
   
        owner = ((ClaimsIdentity)User.Identity).FindFirst(ClaimTypes.NameIdentifier).Value;
   
    **Belangrijke**: geen opmerkingen bij de code in de `ToDoListDataAPI` methode; doet u dat later voor de service principal verificatie zelfstudie.

### <a name="deploy-the-todolistapi-project-to-azure"></a>Het project ToDoListAPI implementeren in Azure
1. In **Solution Explorer**, met de rechtermuisknop op het project ToDoListAPI en klik vervolgens op **publiceren**.
2. Klik op **Publish**.
   
    Visual Studio implementeert het project en opent een browservenster met de basis-URL van de API-app.
3. Sluit de browser.

### <a name="test-the-application"></a>De toepassing testen
1. Ga naar de URL van de web-app **met behulp van HTTPS niet HTTP**.
2. Klik op de **To Do List** tabblad.
   
    U wordt gevraagd om aan te melden.
3. Aanmelden met de referenties van een gebruiker in uw AAD-tenant.
4. De **To Do List** pagina wordt weergegeven.
   
   ![Takenlijstpagina](./media/app-service-api-dotnet-user-principal-auth/webappindex.png)
   
   Er is geen taakitems worden weergegeven omdat tot op heden alle eigenaar zijn ' * '. Nu de middelste laag items voor de aangemelde gebruiker vraagt en geen nog zijn gemaakt.
5. Toevoegen van nieuwe taakitems om te controleren of de toepassing werkt.
6. In een ander browservenster, Ga naar de Swagger-gebruikersinterface URL voor de ToDoListDataAPI-API-app en klik **ToDoList > ophalen**. Geef een sterretje voor de `owner` parameter en klik vervolgens op **Try it out in**.
   
   Het antwoord ziet u dat de nieuwe taakitems de werkelijke hebben gebruikers-ID in de eigenschap Owner Azure AD.
   
   ![Eigenaar-ID in JSON-antwoord](./media/app-service-api-dotnet-user-principal-auth/todolistapiauth.png)

## <a name="building-the-projects-from-scratch"></a>Het bouwen van de projecten maken
De twee Web API-projecten zijn gemaakt met behulp van de **Azure API-App** project sjabloon en de waarden van standaard domeincontroller vervangen door een ToDoList-controller. 

Zie voor meer informatie over het maken van een AngularJS-toepassing voor één pagina met een Web API 2 back-end [handen op Lab: bouwen van een enkele toepassing pagina WACHTWOORDVERIFICATIE met ASP.NET Web API en Angular.js](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs). Zie de volgende bronnen voor meer informatie over het toevoegen van Azure AD verificatiecode op te geven:

* [Apps met Azure AD beveiligen AngularJS één pagina](../active-directory/active-directory-devquickstarts-angular.md).
* [Introductie van ADAL JS v1](http://www.cloudidentity.com/blog/2015/02/19/introducing-adal-js-v1/)

## <a name="troubleshooting"></a>Problemen oplossen
[!INCLUDE [troubleshooting](../../includes/app-service-api-auth-troubleshooting.md)]

* Zorg ervoor dat u en niet door elkaar ToDoListAPI (middelste laag) ToDoListDataAPI (gegevenslaag). Controleer bijvoorbeeld of dat u verificatie toegevoegd aan de middelste laag API-app niet de gegevenslaag. 
* Zorg ervoor dat de broncode van de AngularJS verwijst naar de middelste laag API app-URL (ToDoListAPI, niet ToDoListDataAPI) en de juiste Azure AD-client-ID. 

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe u App Service-verificatie voor een API-app en het aanroepen van de API-app met behulp van de ADAL-JS library. In de volgende zelfstudie leert u hoe u [beveiligde toegang tot uw API-app voor scenario's voor service to service](app-service-api-dotnet-service-principal-auth.md).


---
title: aaaCORS ondersteuning in App Service | Microsoft Docs
description: Meer informatie over hoe toouse CORS in Azure Azure App Service ondersteunen.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 4f980a97-b9f5-4d1d-87ab-82b60bb96e1c
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/27/2016
ms.author: alkarche
ms.openlocfilehash: c229378b75840bc0f7b2eefc3df3031233f9b494
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a>Een API-app van JavaScript gebruiken met CORS
App Service biedt ingebouwde ondersteuning voor [Cross Origin Resource delen (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), waarmee JavaScript-clients toomake tussen domeinen aanroepen tooAPIs die worden gehost in API-apps. App Service kunt u CORS toegang tooyour API configureren zonder de code schrijven in uw API.

Dit artikel bestaat uit twee gedeelten:

* Hallo [hoe tooconfigure CORS](#corsconfig) sectie wordt uitgelegd hoe u algemene tooconfigure CORS voor API-app, web-app of mobiele app. Het is evenveel van toepassing tooall frameworks die worden ondersteund door App Service, waaronder .NET, Node.js en Java. 
* Beginnen met Hallo [u doorgaat zelfstudies .NET-aan de slag Hallo](#tutorialstart) sectie Hallo artikel is een zelfstudie leert u hoe CORS-ondersteuning door te bouwen op wat u hebt gedaan wordt [Hallo eerste API-Apps zelfstudie aan de slag ](app-service-api-dotnet-get-started.md). 

## <a id="corsconfig"></a>Hoe tooconfigure CORS in Azure App Service
U kunt CORS configureren in hello Azure-portal of met behulp van [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) hulpprogramma's.

#### <a name="configure-cors-in-hello-azure-portal"></a>CORS configureren in hello Azure-portal
1. Ga in een browser toohello [Azure-portal](https://portal.azure.com/).
2. Klik op **App Services**, en klik vervolgens op Hallo-naam van uw API-app.
   
    ![De API-app in de portal selecteren](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. In Hallo **instellingen** blade die wordt geopend toohello rechts van Hallo **API-app** blade, zoeken Hallo **API** sectie en klik vervolgens op **CORS**.
   
   ![CORS selecteren op de blade Instellingen](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Voer in het tekstvak Hallo Hallo URL of URL's die u wilt dat tooallow JavaScript-aanroepen toocome uit.

    Bijvoorbeeld, als u uw JavaScript toepassing tooa web-app met de naam todolistangular hebt geïmplementeerd, voert u 'https://todolistangular.azurewebsites.net' in. Als alternatief kunt u een sterretje (*) toospecify dat alle domeinen worden geaccepteerd.


1. Klik op **Opslaan**.
   
   ![Op Opslaan klikken](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Nadat u op **opslaan**, accepteert Hallo API-app JavaScript-aanroepen vanuit Hallo opgegeven URL's.

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a>CORS configureren met de Azure Resource Manager-hulpprogramma's
U kunt CORS ook configureren voor een API-app met behulp van [Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md) in opdrachtregelhulpprogramma's zoals [Azure PowerShell](/powershell/azureps-cmdlets-docs) en Hallo [Azure CLI](../cli-install-nodejs.md). 

Voor een voorbeeld van een Azure Resource Manager-sjabloon die Hallo CORS-eigenschap instelt, opent u Hallo [bestand azuredeploy.json in Hallo-opslagplaats voor de voorbeeldtoepassing uit deze zelfstudie](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json). Hallo-sectie van het Hallo-sjabloon die lijkt op het volgende voorbeeld Hallo vinden:

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <a id="tutorialstart"></a>U kunt doorgaan Hallo .NET aan de slag-zelfstudie
Als u Hallo Node.js of Java reeks aan de slag voor API-apps volgt, hebt u voltooide Hallo gestart reeks ophalen. Overslaan toohello [Vervolgstappen](#next-steps) sectie toofind-suggesties voor meer informatiebronnen over API-Apps.

Hallo rest van dit artikel is een vervolg van de reeks aan de slag met .NET Hallo en wordt ervan uitgegaan dat u met succes voltooid [Hallo eerste zelfstudie](app-service-api-dotnet-get-started.md).

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a>Hallo project tooa nieuwe web-app ToDoListAngular implementeren
In [Hallo eerste zelfstudie](app-service-api-dotnet-get-started.md), u een van de middelste laag API-app en een API app voor de gegevenslaag gemaakt. In deze zelfstudie maakt u een web-app (SPA) single-page application die aanroepen Hallo middelste laag API-app. U hebt tooenable CORS op Hallo middelste laag API-app voor Hallo SPA toowork. 

In Hallo [voorbeeldtoepassing ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), Hallo ToDoListAngular project is een eenvoudige AngularJS-client die het ToDoListAPI Web API-project voor Hallo middelste laag aanroept. JavaScript-code in Hallo Hallo *app/scripts/todoListSvc.js* bestand Hallo-API aanroept met behulp van Hallo AngularJS HTTP-provider. 

        angular.module('todoApp')
        .factory('todoListSvc', ['$http', function ($http) {

            $http.defaults.useXDomain = true;
            delete $http.defaults.headers.common['X-Requested-With']; 

            return {
                getItems : function(){
                    return $http.get(apiEndpoint + '/api/TodoList');
                },

                /* Get by ID, Put, and Delete methods not shown */

                postItem : function(item){
                    return $http.post(apiEndpoint + '/api/TodoList', item);
                }
            };
        }]);

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a>Een nieuwe web-app voor Hallo ToDoListAngular project maken
Hallo toocreate procedure een nieuwe App Service-web-app en het implementeren van een project tooit is vergelijkbaar toowhat die u hebt gezien voor [maken en implementeren van een API-app in de eerste zelfstudie van deze reeks Hallo](app-service-api-dotnet-get-started.md#createapiapp). Hallo alleen verschil dat Hallo app-type is is **Web-App** in plaats van **API-App**.  Zie voor schermafbeeldingen van Hallo dialoogvensters, 

1. In **Solution Explorer**, met de rechtermuisknop op Hallo ToDoListAngular project en klik vervolgens op **publiceren**.
2. In Hallo **profiel** tabblad Hallo **webpublicatie** wizard, klikt u op **Microsoft Azure App Service**.
3. In Hallo **App Service** in het dialoogvenster, klikt u op **nieuw**.
4. In Hallo **Hosting** tabblad Hallo **Create App Service** dialoogvenster Voer een **Web-Appnaam** die uniek is in Hallo *azurewebsites.net* een domein. 
5. Kies hello Azure **abonnement** gewenste toowork met.
6. In Hallo **resourcegroep** vervolgkeuzelijst Hallo Kies dezelfde resourcegroep die u eerder hebt gemaakt.
7. In Hallo **App Service-abonnement** vervolgkeuzelijst Kies Hallo hetzelfde abonnement dat u eerder hebt gemaakt. 
8. Klik op **Create**.
   
    Visual Studio maakt Hallo web-app, maakt er een publicatieprofiel voor en geeft weer Hallo **verbinding** stap Hallo **webpublicatie** wizard.
   
    Klik nog niet op **Publish**. Hallo volgende sectie, configureert u Hallo nieuwe web-app toocall Hallo middelste laag API-app die wordt uitgevoerd in App Service. 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a>Hallo-URL voor de middelste laag instellen in instellingen voor web-app
1. Ga toohello [Azure-portal](https://portal.azure.com/), en navigeert u vervolgens toohello **Web-App** blade voor Hallo web-app die u hebt gemaakt (toohost hello front-end) project TodoListAngular.
2. Klik op **Instellingen > Toepassingsinstellingen**.
3. In Hallo **appinstellingen** sectie, voeg Hallo volgende sleutel en waarde:
   
   | Sleutel | Waarde | Voorbeeld |
   | --- | --- | --- |
   | toDoListAPIURL |https://{de naam van uw API-app voor de middelste laag}.azurewebsites.net |https://todolistapi0121.azurewebsites.net |
4. Klik op **Opslaan**.
   
    Wanneer het Hallo-code wordt uitgevoerd in Azure, overschrijft deze waarde Hallo localhost-URL die zich in Hallo *Web.config* bestand. 
   
    Hallo-code die de instellingswaarde Hallo krijgt *index.cshtml*:
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    Hallo-code in *todoListSvc.js* Hallo-instelling wordt gebruikt:
   
        return {
            getItems : function(){
                return $http.get(apiEndpoint + '/api/TodoList');
            },
            getItem : function(id){
                return $http.get(apiEndpoint + '/api/TodoList/' + id);
            },
            postItem : function(item){
                return $http.post(apiEndpoint + '/api/TodoList', item);
            },
            putItem : function(item){
                return $http.put(apiEndpoint + '/api/TodoList/', item);
            },
            deleteItem : function(id){
                return $http({
                    method: 'DELETE',
                    url: apiEndpoint + '/api/TodoList/' + id
                });
            }
        };

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a>Hallo web project toohello nieuwe web-app ToDoListAngular implementeren
* In Visual Studio in Hallo **verbinding** stap Hallo **webpublicatie** wizard, klikt u op **publiceren**.
  
   Visual Studio Hallo ToDoListAngular project toohello nieuwe web-app implementeert en een URL van de browser toohello van Hallo web-app wordt geopend. 

### <a name="test-hello-application-without-cors-enabled"></a>Hallo toepassing testen zonder dat CORS is ingeschakeld
1. Open in uw browser hulpprogramma's voor ontwikkelaars Hallo-consolevenster.
2. In het browservenster Hallo die Hallo AngularJS UI wordt weergegeven, klikt u op Hallo **tooDo lijst** koppeling.
   
    Hallo JavaScript-code probeert toocall Hallo middelste laag API-app, maar Hallo-aanroep is mislukt omdat Hallo-front-end wordt uitgevoerd in een ander domein dan Hallo terug end. Hallo van de Console hulpprogramma's voor ontwikkelaars browservenster weergegeven een cross-origin-foutbericht.
   
    ![Cross-origin-foutbericht](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a>CORS configureren voor de middelste laag Hallo API-app
In deze sectie configureert u Hallo CORS-instelling in Azure voor Hallo middelste laag API-app ToDoListAPI. Deze instelling kunt Hallo middelste laag API app tooreceive JavaScript-aanroepen vanuit Hallo web-app die u hebt gemaakt voor de project ToDoListAngular Hallo.

1. Ga in een browser toohello [Azure-portal](https://portal.azure.com/).
2. Klik op **App Services**, en klik vervolgens op Hallo ToDoListAPI (middelste laag) API-app.
   
    ![De API-app in de portal selecteren](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. In Hallo **instellingen** blade die wordt geopend toohello rechts van Hallo **API-app** blade, zoeken Hallo **API** sectie en klik vervolgens op **CORS**.
   
   ![CORS selecteren in de portal](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. Voer in het tekstvak hello, Hallo-URL voor Hallo ToDoListAngular (front-end) web-app. Bijvoorbeeld, u Hallo project tooa web-app ToDoListAngular met de naam todolistangular0121 hebt geïmplementeerd, staat u aanroepen toe van Hallo URL `https://todolistangular0121.azurewebsites.net`.
   
   Als alternatief kunt u een sterretje (*) toospecify dat alle domeinen worden geaccepteerd.
5. Klik op **Opslaan**.
   
   ![Op Opslaan klikken](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   Nadat u op **opslaan**, accepteert Hallo API-app JavaScript-aanroepen vanuit Hallo URL opgegeven. In deze schermafbeelding accepteert Hallo API-app ToDoListAPI0223 JavaScript-clientaanroepen van web-app ToDoListAngular Hallo.

### <a name="test-hello-application-with-cors-enabled"></a>Hallo toepassing testen met CORS ingeschakeld
* Open een browser toohello HTTPS-URL van Hallo web-app. 
  
    Deze toepassing hello kunt u weergeven, toevoegen, bewerken en verwijderen van taken. 
  
    ![tooDo lijstpagina van de voorbeeld-app](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a>App Service CORS versus Web API CORS
In een Web API-project, installeert u Hallo [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet-pakket toospecify in welke domeinen uw API JavaScript-accepteert van aanroepen code.

Ondersteuning voor Web API CORS biedt meer flexibiliteit dan ondersteuning voor App Service CORS. Zo kunt u in de code voor verschillende actiemethoden verschillende toegestane bronnen opgeven. Voor App Service CORS kunt u voor alle methoden van uw API-app slechts één set toegestane bronnen opgeven.

> [!NOTE]
> Probeer niet toouse zowel Web API CORS en App Service CORS in één API-app. Doet u dit toch, dan krijgt App Service CORS voorrang en heeft Web API CORS geen effect. Bijvoorbeeld, als u één brondomein in App Service inschakelt en inschakelen van alle domeinen in uw Web-API-code, accepteert uw Azure-API-app alleen aanroepen vanuit Hallo domein dat u in Azure hebt opgegeven.
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a>Hoe tooenable CORS in Web-API-code
Hallo stappen geven een overzicht van Hallo-proces voor het inschakelen van Web API CORS-ondersteuning. Zie [Cross-origin-aanvragen inschakelen in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api) voor meer informatie.

1. Installeren in een Web-API-project Hallo [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet-pakket.
2. Omvatten een `config.EnableCors()` coderegel in Hallo **registreren** methode Hallo **WebApiConfig** klasse, zoals in het volgende voorbeeld Hallo. 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // hello following line enables you toocontrol CORS by using Web API code
                config.EnableCors();
   
                // Web API routes
                config.MapHttpAttributeRoutes();
   
                config.Routes.MapHttpRoute(
                    name: "DefaultApi",
                    routeTemplate: "api/{controller}/{id}",
                    defaults: new { id = RouteParameter.Optional }
                );
            }
        }
3. Voeg in uw Web-API-controller een `using` -instructie voor Hallo `System.Web.Http.Cors` naamruimte, en voeg Hallo `EnableCors` kenmerk toohello-controller klasse of tooindividual actiemethoden. In de Hallo voorbeeld te volgen, geldt CORS-ondersteuning toohello gehele controller.
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a>Azure API Management gebruiken met API-apps
Als u Azure API Management met een API-app gebruikt, configureert u CORS in API Management in plaats van in Hallo API-app. Zie voor meer informatie Hallo resources te volgen:

* [Overzicht van Azure API Management (video: CORS begint bij 12:10)](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [API Management-beleid voor meerdere domeinen](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a>Problemen oplossen
Als u een probleem ervaart tijdens het doorlopen van deze zelfstudie, vindt hier u enkele ideeën voor probleemoplossing.

* Zorg ervoor dat u de meest recente versie Hallo Hallo [Azure SDK voor .NET voor Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).
* Zorg ervoor dat u hebt ingevoerd `https` in Hallo CORS-instelling en zorg ervoor dat u gebruikt `https` toorun Hallo front-end web-app.
* Zorg ervoor dat het ingevoerde Hallo CORS-instelling in Hallo middelste laag API-app, niet in Hallo front-end web-app.
* Als u CORS in de toepassingscode en Azure App Service configureren bent, houd er rekening mee dat Hallo-App Service CORS-instelling overschrijft wat u doet in de toepassingscode. 

Zie toolearn meer informatie over de functies van Visual Studio die probleemoplossing vereenvoudigen [problemen Azure App Service-apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u gezien hoe App Service CORS tooenable ondersteunen, zodat de client-JavaScript-code een API kan aanroepen in een ander domein. meer informatie over API-apps Lees Hallo toolearn [tooauthentication Inleiding in App Service](../app-service/app-service-authentication-overview.md), en ga toohello [gebruikersverificatie voor API-apps](app-service-api-dotnet-user-principal-auth.md) zelfstudie.


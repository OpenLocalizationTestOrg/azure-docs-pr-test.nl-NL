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
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="68ff6-103">Een API-app van JavaScript gebruiken met CORS</span><span class="sxs-lookup"><span data-stu-id="68ff6-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="68ff6-104">App Service biedt ingebouwde ondersteuning voor [Cross Origin Resource delen (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), waarmee JavaScript-clients toomake tussen domeinen aanroepen tooAPIs die worden gehost in API-apps.</span><span class="sxs-lookup"><span data-stu-id="68ff6-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients toomake cross-domain calls tooAPIs that are hosted in API apps.</span></span> <span data-ttu-id="68ff6-105">App Service kunt u CORS toegang tooyour API configureren zonder de code schrijven in uw API.</span><span class="sxs-lookup"><span data-stu-id="68ff6-105">App Service lets you configure CORS access tooyour API without writing any code in your API.</span></span>

<span data-ttu-id="68ff6-106">Dit artikel bestaat uit twee gedeelten:</span><span class="sxs-lookup"><span data-stu-id="68ff6-106">This article contains two sections:</span></span>

* <span data-ttu-id="68ff6-107">Hallo [hoe tooconfigure CORS](#corsconfig) sectie wordt uitgelegd hoe u algemene tooconfigure CORS voor API-app, web-app of mobiele app.</span><span class="sxs-lookup"><span data-stu-id="68ff6-107">hello [How tooconfigure CORS](#corsconfig) section explains in general how tooconfigure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="68ff6-108">Het is evenveel van toepassing tooall frameworks die worden ondersteund door App Service, waaronder .NET, Node.js en Java.</span><span class="sxs-lookup"><span data-stu-id="68ff6-108">It applies equally tooall frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="68ff6-109">Beginnen met Hallo [u doorgaat zelfstudies .NET-aan de slag Hallo](#tutorialstart) sectie Hallo artikel is een zelfstudie leert u hoe CORS-ondersteuning door te bouwen op wat u hebt gedaan wordt [Hallo eerste API-Apps zelfstudie aan de slag ](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="68ff6-109">Starting with hello [Continuing hello .NET getting-started tutorials](#tutorialstart) section, hello article is a tutorial that demonstrates CORS support by building on what you did in [hello first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="68ff6-110"><a id="corsconfig"></a>Hoe tooconfigure CORS in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="68ff6-110"><a id="corsconfig"></a> How tooconfigure CORS in Azure App Service</span></span>
<span data-ttu-id="68ff6-111">U kunt CORS configureren in hello Azure-portal of met behulp van [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="68ff6-111">You can configure CORS in hello Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-hello-azure-portal"></a><span data-ttu-id="68ff6-112">CORS configureren in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="68ff6-112">Configure CORS in hello Azure portal</span></span>
1. <span data-ttu-id="68ff6-113">Ga in een browser toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68ff6-113">In a browser go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="68ff6-114">Klik op **App Services**, en klik vervolgens op Hallo-naam van uw API-app.</span><span class="sxs-lookup"><span data-stu-id="68ff6-114">Click **App Services**, and then click hello name of your API app.</span></span>
   
    ![De API-app in de portal selecteren](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="68ff6-116">In Hallo **instellingen** blade die wordt geopend toohello rechts van Hallo **API-app** blade, zoeken Hallo **API** sectie en klik vervolgens op **CORS**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-116">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![CORS selecteren op de blade Instellingen](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="68ff6-118">Voer in het tekstvak Hallo Hallo URL of URL's die u wilt dat tooallow JavaScript-aanroepen toocome uit.</span><span class="sxs-lookup"><span data-stu-id="68ff6-118">In hello text box enter hello URL or URLs that you want tooallow JavaScript calls toocome from.</span></span>

    <span data-ttu-id="68ff6-119">Bijvoorbeeld, als u uw JavaScript toepassing tooa web-app met de naam todolistangular hebt geïmplementeerd, voert u 'https://todolistangular.azurewebsites.net' in.</span><span class="sxs-lookup"><span data-stu-id="68ff6-119">For example, if you deployed your JavaScript application tooa web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="68ff6-120">Als alternatief kunt u een sterretje (*) toospecify dat alle domeinen worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="68ff6-120">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="68ff6-121">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-121">Click **Save**.</span></span>
   
   ![Op Opslaan klikken](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="68ff6-123">Nadat u op **opslaan**, accepteert Hallo API-app JavaScript-aanroepen vanuit Hallo opgegeven URL's.</span><span class="sxs-lookup"><span data-stu-id="68ff6-123">After you click **Save**, hello API app will accept JavaScript calls from hello specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="68ff6-124">CORS configureren met de Azure Resource Manager-hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="68ff6-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="68ff6-125">U kunt CORS ook configureren voor een API-app met behulp van [Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md) in opdrachtregelhulpprogramma's zoals [Azure PowerShell](/powershell/azureps-cmdlets-docs) en Hallo [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="68ff6-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and hello [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="68ff6-126">Voor een voorbeeld van een Azure Resource Manager-sjabloon die Hallo CORS-eigenschap instelt, opent u Hallo [bestand azuredeploy.json in Hallo-opslagplaats voor de voorbeeldtoepassing uit deze zelfstudie](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="68ff6-126">For an example of an Azure Resource Manager template that sets hello CORS property, open hello [azuredeploy.json file in hello repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="68ff6-127">Hallo-sectie van het Hallo-sjabloon die lijkt op het volgende voorbeeld Hallo vinden:</span><span class="sxs-lookup"><span data-stu-id="68ff6-127">Find hello section of hello template that looks like hello following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="68ff6-128"><a id="tutorialstart"></a>U kunt doorgaan Hallo .NET aan de slag-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="68ff6-128"><a id="tutorialstart"></a> Continuing hello .NET getting-started tutorial</span></span>
<span data-ttu-id="68ff6-129">Als u Hallo Node.js of Java reeks aan de slag voor API-apps volgt, hebt u voltooide Hallo gestart reeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="68ff6-129">If you are following hello Node.js or Java getting-started series for API apps, you have completed hello getting started series.</span></span> <span data-ttu-id="68ff6-130">Overslaan toohello [Vervolgstappen](#next-steps) sectie toofind-suggesties voor meer informatiebronnen over API-Apps.</span><span class="sxs-lookup"><span data-stu-id="68ff6-130">Skip toohello [Next steps](#next-steps) section toofind suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="68ff6-131">Hallo rest van dit artikel is een vervolg van de reeks aan de slag met .NET Hallo en wordt ervan uitgegaan dat u met succes voltooid [Hallo eerste zelfstudie](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="68ff6-131">hello remainder of this article is a continuation of hello .NET getting-started series and assumes that you successfully completed [hello first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-hello-todolistangular-project-tooa-new-web-app"></a><span data-ttu-id="68ff6-132">Hallo project tooa nieuwe web-app ToDoListAngular implementeren</span><span class="sxs-lookup"><span data-stu-id="68ff6-132">Deploy hello ToDoListAngular project tooa new web app</span></span>
<span data-ttu-id="68ff6-133">In [Hallo eerste zelfstudie](app-service-api-dotnet-get-started.md), u een van de middelste laag API-app en een API app voor de gegevenslaag gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68ff6-133">In [hello first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="68ff6-134">In deze zelfstudie maakt u een web-app (SPA) single-page application die aanroepen Hallo middelste laag API-app.</span><span class="sxs-lookup"><span data-stu-id="68ff6-134">In this tutorial you create a single-page application (SPA) web app that calls hello middle tier API app.</span></span> <span data-ttu-id="68ff6-135">U hebt tooenable CORS op Hallo middelste laag API-app voor Hallo SPA toowork.</span><span class="sxs-lookup"><span data-stu-id="68ff6-135">For hello SPA toowork you have tooenable CORS on hello middle tier API app.</span></span> 

<span data-ttu-id="68ff6-136">In Hallo [voorbeeldtoepassing ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), Hallo ToDoListAngular project is een eenvoudige AngularJS-client die het ToDoListAPI Web API-project voor Hallo middelste laag aanroept.</span><span class="sxs-lookup"><span data-stu-id="68ff6-136">In hello [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), hello ToDoListAngular project is a simple AngularJS client that calls hello middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="68ff6-137">JavaScript-code in Hallo Hallo *app/scripts/todoListSvc.js* bestand Hallo-API aanroept met behulp van Hallo AngularJS HTTP-provider.</span><span class="sxs-lookup"><span data-stu-id="68ff6-137">hello JavaScript code in hello *app/scripts/todoListSvc.js* file calls hello API by using hello AngularJS HTTP provider.</span></span> 

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

### <a name="create-a-new-web-app-for-hello-todolistangular-project"></a><span data-ttu-id="68ff6-138">Een nieuwe web-app voor Hallo ToDoListAngular project maken</span><span class="sxs-lookup"><span data-stu-id="68ff6-138">Create a new web app for hello ToDoListAngular project</span></span>
<span data-ttu-id="68ff6-139">Hallo toocreate procedure een nieuwe App Service-web-app en het implementeren van een project tooit is vergelijkbaar toowhat die u hebt gezien voor [maken en implementeren van een API-app in de eerste zelfstudie van deze reeks Hallo](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="68ff6-139">hello procedure toocreate a new App Service web app and deploy a project tooit is similar toowhat you saw for [creating and deploying an API app in hello first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="68ff6-140">Hallo alleen verschil dat Hallo app-type is is **Web-App** in plaats van **API-App**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-140">hello only difference is that hello app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="68ff6-141">Zie voor schermafbeeldingen van Hallo dialoogvensters,</span><span class="sxs-lookup"><span data-stu-id="68ff6-141">For screen shots of hello dialogs, see</span></span> 

1. <span data-ttu-id="68ff6-142">In **Solution Explorer**, met de rechtermuisknop op Hallo ToDoListAngular project en klik vervolgens op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-142">In **Solution Explorer**, right-click hello ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="68ff6-143">In Hallo **profiel** tabblad Hallo **webpublicatie** wizard, klikt u op **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-143">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="68ff6-144">In Hallo **App Service** in het dialoogvenster, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-144">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="68ff6-145">In Hallo **Hosting** tabblad Hallo **Create App Service** dialoogvenster Voer een **Web-Appnaam** die uniek is in Hallo *azurewebsites.net* een domein.</span><span class="sxs-lookup"><span data-stu-id="68ff6-145">In hello **Hosting** tab of hello **Create App Service** dialog box, enter a **Web App Name** that is unique in hello *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="68ff6-146">Kies hello Azure **abonnement** gewenste toowork met.</span><span class="sxs-lookup"><span data-stu-id="68ff6-146">Choose hello Azure **Subscription** you want toowork with.</span></span>
6. <span data-ttu-id="68ff6-147">In Hallo **resourcegroep** vervolgkeuzelijst Hallo Kies dezelfde resourcegroep die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68ff6-147">In hello **Resource Group** drop-down list, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="68ff6-148">In Hallo **App Service-abonnement** vervolgkeuzelijst Kies Hallo hetzelfde abonnement dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="68ff6-148">In hello **App Service Plan** drop-down list, choose hello same plan you created earlier.</span></span> 
8. <span data-ttu-id="68ff6-149">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-149">Click **Create**.</span></span>
   
    <span data-ttu-id="68ff6-150">Visual Studio maakt Hallo web-app, maakt er een publicatieprofiel voor en geeft weer Hallo **verbinding** stap Hallo **webpublicatie** wizard.</span><span class="sxs-lookup"><span data-stu-id="68ff6-150">Visual Studio creates hello web app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="68ff6-151">Klik nog niet op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="68ff6-152">Hallo volgende sectie, configureert u Hallo nieuwe web-app toocall Hallo middelste laag API-app die wordt uitgevoerd in App Service.</span><span class="sxs-lookup"><span data-stu-id="68ff6-152">In hello following section, you configure hello new web app toocall hello middle tier API app that is running in App Service.</span></span> 

### <a name="set-hello-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="68ff6-153">Hallo-URL voor de middelste laag instellen in instellingen voor web-app</span><span class="sxs-lookup"><span data-stu-id="68ff6-153">Set hello middle tier URL in web app settings</span></span>
1. <span data-ttu-id="68ff6-154">Ga toohello [Azure-portal](https://portal.azure.com/), en navigeert u vervolgens toohello **Web-App** blade voor Hallo web-app die u hebt gemaakt (toohost hello front-end) project TodoListAngular.</span><span class="sxs-lookup"><span data-stu-id="68ff6-154">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **Web App** blade for hello web app that you created toohost hello TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="68ff6-155">Klik op **Instellingen > Toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="68ff6-156">In Hallo **appinstellingen** sectie, voeg Hallo volgende sleutel en waarde:</span><span class="sxs-lookup"><span data-stu-id="68ff6-156">In hello **App settings** section, add hello following key and value:</span></span>
   
   | <span data-ttu-id="68ff6-157">Sleutel</span><span class="sxs-lookup"><span data-stu-id="68ff6-157">Key</span></span> | <span data-ttu-id="68ff6-158">Waarde</span><span class="sxs-lookup"><span data-stu-id="68ff6-158">Value</span></span> | <span data-ttu-id="68ff6-159">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="68ff6-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="68ff6-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="68ff6-160">toDoListAPIURL</span></span> |<span data-ttu-id="68ff6-161">https://{de naam van uw API-app voor de middelste laag}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="68ff6-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="68ff6-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="68ff6-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="68ff6-163">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-163">Click **Save**.</span></span>
   
    <span data-ttu-id="68ff6-164">Wanneer het Hallo-code wordt uitgevoerd in Azure, overschrijft deze waarde Hallo localhost-URL die zich in Hallo *Web.config* bestand.</span><span class="sxs-lookup"><span data-stu-id="68ff6-164">When hello code runs in Azure, this value overrides hello localhost URL that is in hello *Web.config* file.</span></span> 
   
    <span data-ttu-id="68ff6-165">Hallo-code die de instellingswaarde Hallo krijgt *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="68ff6-165">hello code that gets hello setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="68ff6-166">Hallo-code in *todoListSvc.js* Hallo-instelling wordt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="68ff6-166">hello code in *todoListSvc.js* uses hello setting:</span></span>
   
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

### <a name="deploy-hello-todolistangular-web-project-toohello-new-web-app"></a><span data-ttu-id="68ff6-167">Hallo web project toohello nieuwe web-app ToDoListAngular implementeren</span><span class="sxs-lookup"><span data-stu-id="68ff6-167">Deploy hello ToDoListAngular web project toohello new web app</span></span>
* <span data-ttu-id="68ff6-168">In Visual Studio in Hallo **verbinding** stap Hallo **webpublicatie** wizard, klikt u op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-168">In Visual Studio, in hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="68ff6-169">Visual Studio Hallo ToDoListAngular project toohello nieuwe web-app implementeert en een URL van de browser toohello van Hallo web-app wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="68ff6-169">Visual Studio deploys hello ToDoListAngular project toohello new web app and opens a browser toohello URL of hello web app.</span></span> 

### <a name="test-hello-application-without-cors-enabled"></a><span data-ttu-id="68ff6-170">Hallo toepassing testen zonder dat CORS is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="68ff6-170">Test hello application without CORS enabled</span></span>
1. <span data-ttu-id="68ff6-171">Open in uw browser hulpprogramma's voor ontwikkelaars Hallo-consolevenster.</span><span class="sxs-lookup"><span data-stu-id="68ff6-171">In your browser Developer Tools, open hello Console window.</span></span>
2. <span data-ttu-id="68ff6-172">In het browservenster Hallo die Hallo AngularJS UI wordt weergegeven, klikt u op Hallo **tooDo lijst** koppeling.</span><span class="sxs-lookup"><span data-stu-id="68ff6-172">In hello browser window that displays hello AngularJS UI, click hello **tooDo List** link.</span></span>
   
    <span data-ttu-id="68ff6-173">Hallo JavaScript-code probeert toocall Hallo middelste laag API-app, maar Hallo-aanroep is mislukt omdat Hallo-front-end wordt uitgevoerd in een ander domein dan Hallo terug end.</span><span class="sxs-lookup"><span data-stu-id="68ff6-173">hello JavaScript code tries toocall hello middle tier API app, but hello call fails because hello front end is running in a different domain than hello back end.</span></span> <span data-ttu-id="68ff6-174">Hallo van de Console hulpprogramma's voor ontwikkelaars browservenster weergegeven een cross-origin-foutbericht.</span><span class="sxs-lookup"><span data-stu-id="68ff6-174">hello browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Cross-origin-foutbericht](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-hello-middle-tier-api-app"></a><span data-ttu-id="68ff6-176">CORS configureren voor de middelste laag Hallo API-app</span><span class="sxs-lookup"><span data-stu-id="68ff6-176">Configure CORS for hello middle tier API app</span></span>
<span data-ttu-id="68ff6-177">In deze sectie configureert u Hallo CORS-instelling in Azure voor Hallo middelste laag API-app ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="68ff6-177">In this section, you configure hello CORS setting in Azure for hello middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="68ff6-178">Deze instelling kunt Hallo middelste laag API app tooreceive JavaScript-aanroepen vanuit Hallo web-app die u hebt gemaakt voor de project ToDoListAngular Hallo.</span><span class="sxs-lookup"><span data-stu-id="68ff6-178">This setting will allow hello middle tier API app tooreceive JavaScript calls from hello web app that you created for hello ToDoListAngular project.</span></span>

1. <span data-ttu-id="68ff6-179">Ga in een browser toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68ff6-179">In a browser, go toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="68ff6-180">Klik op **App Services**, en klik vervolgens op Hallo ToDoListAPI (middelste laag) API-app.</span><span class="sxs-lookup"><span data-stu-id="68ff6-180">Click **App Services**, and then click hello ToDoListAPI (middle tier) API app.</span></span>
   
    ![De API-app in de portal selecteren](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="68ff6-182">In Hallo **instellingen** blade die wordt geopend toohello rechts van Hallo **API-app** blade, zoeken Hallo **API** sectie en klik vervolgens op **CORS**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-182">In hello **Settings** blade that opens toohello right of hello **API app** blade, find hello **API** section, and then click **CORS**.</span></span>
   
   ![CORS selecteren in de portal](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="68ff6-184">Voer in het tekstvak hello, Hallo-URL voor Hallo ToDoListAngular (front-end) web-app.</span><span class="sxs-lookup"><span data-stu-id="68ff6-184">In hello text box, enter hello URL for hello ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="68ff6-185">Bijvoorbeeld, u Hallo project tooa web-app ToDoListAngular met de naam todolistangular0121 hebt geïmplementeerd, staat u aanroepen toe van Hallo URL `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="68ff6-185">For example, if you deployed hello ToDoListAngular project tooa web app named todolistangular0121, allow calls from hello URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="68ff6-186">Als alternatief kunt u een sterretje (*) toospecify dat alle domeinen worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="68ff6-186">As an alternative, you can enter an asterisk (*) toospecify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="68ff6-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="68ff6-187">Click **Save**.</span></span>
   
   ![Op Opslaan klikken](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="68ff6-189">Nadat u op **opslaan**, accepteert Hallo API-app JavaScript-aanroepen vanuit Hallo URL opgegeven.</span><span class="sxs-lookup"><span data-stu-id="68ff6-189">After you click **Save**, hello API app will accept JavaScript calls from hello specified URL.</span></span> <span data-ttu-id="68ff6-190">In deze schermafbeelding accepteert Hallo API-app ToDoListAPI0223 JavaScript-clientaanroepen van web-app ToDoListAngular Hallo.</span><span class="sxs-lookup"><span data-stu-id="68ff6-190">In this screen shot, hello ToDoListAPI0223 API app will accept JavaScript client calls from hello ToDoListAngular web app.</span></span>

### <a name="test-hello-application-with-cors-enabled"></a><span data-ttu-id="68ff6-191">Hallo toepassing testen met CORS ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="68ff6-191">Test hello application with CORS enabled</span></span>
* <span data-ttu-id="68ff6-192">Open een browser toohello HTTPS-URL van Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="68ff6-192">Open a browser toohello HTTPS URL of hello web app.</span></span> 
  
    <span data-ttu-id="68ff6-193">Deze toepassing hello kunt u weergeven, toevoegen, bewerken en verwijderen van taken.</span><span class="sxs-lookup"><span data-stu-id="68ff6-193">This time hello application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![tooDo lijstpagina van de voorbeeld-app](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="68ff6-195">App Service CORS versus Web API CORS</span><span class="sxs-lookup"><span data-stu-id="68ff6-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="68ff6-196">In een Web API-project, installeert u Hallo [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet-pakket toospecify in welke domeinen uw API JavaScript-accepteert van aanroepen code.</span><span class="sxs-lookup"><span data-stu-id="68ff6-196">In a Web API project, you can install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package toospecify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="68ff6-197">Ondersteuning voor Web API CORS biedt meer flexibiliteit dan ondersteuning voor App Service CORS.</span><span class="sxs-lookup"><span data-stu-id="68ff6-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="68ff6-198">Zo kunt u in de code voor verschillende actiemethoden verschillende toegestane bronnen opgeven. Voor App Service CORS kunt u voor alle methoden van uw API-app slechts één set toegestane bronnen opgeven.</span><span class="sxs-lookup"><span data-stu-id="68ff6-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="68ff6-199">Probeer niet toouse zowel Web API CORS en App Service CORS in één API-app.</span><span class="sxs-lookup"><span data-stu-id="68ff6-199">Don't try toouse both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="68ff6-200">Doet u dit toch, dan krijgt App Service CORS voorrang en heeft Web API CORS geen effect.</span><span class="sxs-lookup"><span data-stu-id="68ff6-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="68ff6-201">Bijvoorbeeld, als u één brondomein in App Service inschakelt en inschakelen van alle domeinen in uw Web-API-code, accepteert uw Azure-API-app alleen aanroepen vanuit Hallo domein dat u in Azure hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="68ff6-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from hello domain you specified in Azure.</span></span>
> 
> 

### <a name="how-tooenable-cors-in-web-api-code"></a><span data-ttu-id="68ff6-202">Hoe tooenable CORS in Web-API-code</span><span class="sxs-lookup"><span data-stu-id="68ff6-202">How tooenable CORS in Web API code</span></span>
<span data-ttu-id="68ff6-203">Hallo stappen geven een overzicht van Hallo-proces voor het inschakelen van Web API CORS-ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="68ff6-203">hello following steps summarize hello process for enabling Web API CORS support.</span></span> <span data-ttu-id="68ff6-204">Zie [Cross-origin-aanvragen inschakelen in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="68ff6-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="68ff6-205">Installeren in een Web-API-project Hallo [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="68ff6-205">In a Web API project, install hello [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="68ff6-206">Omvatten een `config.EnableCors()` coderegel in Hallo **registreren** methode Hallo **WebApiConfig** klasse, zoals in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="68ff6-206">Include a `config.EnableCors()` line of code in hello **Register** method of hello **WebApiConfig** class, as in hello following example.</span></span> 
   
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
3. <span data-ttu-id="68ff6-207">Voeg in uw Web-API-controller een `using` -instructie voor Hallo `System.Web.Http.Cors` naamruimte, en voeg Hallo `EnableCors` kenmerk toohello-controller klasse of tooindividual actiemethoden.</span><span class="sxs-lookup"><span data-stu-id="68ff6-207">In your Web API controller, add a `using` statement for hello `System.Web.Http.Cors` namespace, and add hello `EnableCors` attribute toohello controller class or tooindividual action methods.</span></span> <span data-ttu-id="68ff6-208">In de Hallo voorbeeld te volgen, geldt CORS-ondersteuning toohello gehele controller.</span><span class="sxs-lookup"><span data-stu-id="68ff6-208">In hello following example, CORS support applies toohello entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="68ff6-209">Azure API Management gebruiken met API-apps</span><span class="sxs-lookup"><span data-stu-id="68ff6-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="68ff6-210">Als u Azure API Management met een API-app gebruikt, configureert u CORS in API Management in plaats van in Hallo API-app.</span><span class="sxs-lookup"><span data-stu-id="68ff6-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in hello API app.</span></span> <span data-ttu-id="68ff6-211">Zie voor meer informatie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="68ff6-211">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="68ff6-212">Overzicht van Azure API Management (video: CORS begint bij 12:10)</span><span class="sxs-lookup"><span data-stu-id="68ff6-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="68ff6-213">API Management-beleid voor meerdere domeinen</span><span class="sxs-lookup"><span data-stu-id="68ff6-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="68ff6-214">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="68ff6-214">Troubleshooting</span></span>
<span data-ttu-id="68ff6-215">Als u een probleem ervaart tijdens het doorlopen van deze zelfstudie, vindt hier u enkele ideeën voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="68ff6-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="68ff6-216">Zorg ervoor dat u de meest recente versie Hallo Hallo [Azure SDK voor .NET voor Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="68ff6-216">Make sure that you're using hello latest version of hello [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="68ff6-217">Zorg ervoor dat u hebt ingevoerd `https` in Hallo CORS-instelling en zorg ervoor dat u gebruikt `https` toorun Hallo front-end web-app.</span><span class="sxs-lookup"><span data-stu-id="68ff6-217">Make sure that you entered `https` in hello CORS setting, and make sure that you're using `https` toorun hello front-end web app.</span></span>
* <span data-ttu-id="68ff6-218">Zorg ervoor dat het ingevoerde Hallo CORS-instelling in Hallo middelste laag API-app, niet in Hallo front-end web-app.</span><span class="sxs-lookup"><span data-stu-id="68ff6-218">Make sure that you entered hello CORS setting in hello middle tier API app, not in hello front-end web app.</span></span>
* <span data-ttu-id="68ff6-219">Als u CORS in de toepassingscode en Azure App Service configureren bent, houd er rekening mee dat Hallo-App Service CORS-instelling overschrijft wat u doet in de toepassingscode.</span><span class="sxs-lookup"><span data-stu-id="68ff6-219">If you're configuring CORS in both application code and Azure App Service, note that hello App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="68ff6-220">Zie toolearn meer informatie over de functies van Visual Studio die probleemoplossing vereenvoudigen [problemen Azure App Service-apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="68ff6-220">toolearn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="68ff6-221">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="68ff6-221">Next steps</span></span>
<span data-ttu-id="68ff6-222">In dit artikel hebt u gezien hoe App Service CORS tooenable ondersteunen, zodat de client-JavaScript-code een API kan aanroepen in een ander domein.</span><span class="sxs-lookup"><span data-stu-id="68ff6-222">In this article, you saw how tooenable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="68ff6-223">meer informatie over API-apps Lees Hallo toolearn [tooauthentication Inleiding in App Service](../app-service/app-service-authentication-overview.md), en ga toohello [gebruikersverificatie voor API-apps](app-service-api-dotnet-user-principal-auth.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="68ff6-223">toolearn more about API apps, read hello [introduction tooauthentication in App Service](../app-service/app-service-authentication-overview.md), and then go toohello [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>


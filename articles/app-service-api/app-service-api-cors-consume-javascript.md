---
title: CORS-ondersteuning in App Service | Microsoft Docs
description: Informatie over het gebruik van CORS-ondersteuning in Azure App Service.
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
ms.openlocfilehash: f8373cf5b2e06e6c71bce51cd9e9d5123eea7cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="consume-an-api-app-from-javascript-using-cors"></a><span data-ttu-id="ad0c0-103">Een API-app van JavaScript gebruiken met CORS</span><span class="sxs-lookup"><span data-stu-id="ad0c0-103">Consume an API app from JavaScript using CORS</span></span>
<span data-ttu-id="ad0c0-104">App Service biedt ingebouwde ondersteuning voor [CORS (Cross Origin Resource Sharing)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), waarmee JavaScript-clients aanroepen tussen domeinen kunnen maken naar API's die worden gehost in API-apps.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-104">App Service offers built-in support for [Cross Origin Resource Sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing), which enables JavaScript clients to make cross-domain calls to APIs that are hosted in API apps.</span></span> <span data-ttu-id="ad0c0-105">Met App Service kunt u CORS-toegang tot uw API configureren zonder dat u in de API code hoeft te schrijven.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-105">App Service lets you configure CORS access to your API without writing any code in your API.</span></span>

<span data-ttu-id="ad0c0-106">Dit artikel bestaat uit twee gedeelten:</span><span class="sxs-lookup"><span data-stu-id="ad0c0-106">This article contains two sections:</span></span>

* <span data-ttu-id="ad0c0-107">Eerst wordt in de sectie [CORS configureren](#corsconfig) in grote lijnen uitgelegd hoe u CORS configureert voor een API-app, web-app of mobiele app.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-107">The [How to configure CORS](#corsconfig) section explains in general how to configure CORS for any API app, web app, or mobile app.</span></span> <span data-ttu-id="ad0c0-108">Deze informatie heeft ook betrekking op alle frameworks die door App Service worden ondersteund, waaronder .NET, Node.js en Java.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-108">It applies equally to all frameworks that are supported by App Service, including .NET, Node.js, and Java.</span></span> 
* <span data-ttu-id="ad0c0-109">Vanaf de sectie [Vervolg van de zelfstudie Aan de slag met .NET](#tutorialstart) is het artikel een zelfstudie. Hierin leert u hoe CORS-ondersteuning wordt toegepast, door voort te bouwen op wat u hebt gedaan in [de eerste zelfstudie Aan de slag met API Apps](app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ad0c0-109">Starting with the [Continuing the .NET getting-started tutorials](#tutorialstart) section, the article is a tutorial that demonstrates CORS support by building on what you did in [the first API Apps getting started tutorial](app-service-api-dotnet-get-started.md).</span></span> 

## <span data-ttu-id="ad0c0-110"><a id="corsconfig"></a>CORS configureren in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ad0c0-110"><a id="corsconfig"></a> How to configure CORS in Azure App Service</span></span>
<span data-ttu-id="ad0c0-111">U kunt CORS configureren in Azure Portal of met behulp van de [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)-hulpprogramma's.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-111">You can configure CORS in the Azure portal or by using [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) tools.</span></span>

#### <a name="configure-cors-in-the-azure-portal"></a><span data-ttu-id="ad0c0-112">CORS configureren in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ad0c0-112">Configure CORS in the Azure portal</span></span>
1. <span data-ttu-id="ad0c0-113">Ga in een browser naar de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ad0c0-113">In a browser go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ad0c0-114">Klik op **App Services** en vervolgens op de naam van de API-app.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-114">Click **App Services**, and then click the name of your API app.</span></span>
   
    ![De API-app in de portal selecteren](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="ad0c0-116">Ga op de blade **Instellingen**, die rechts naast de blade **API-app** wordt geopend, naar de sectie **API** en klik vervolgens op **CORS**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-116">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![CORS selecteren op de blade Instellingen](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="ad0c0-118">Voer in het tekstvak de URL of URL's in waarvan JavaScript-aanroepen afkomstig mogen zijn.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-118">In the text box enter the URL or URLs that you want to allow JavaScript calls to come from.</span></span>

    <span data-ttu-id="ad0c0-119">Als u uw JavaScript-toepassing bijvoorbeeld hebt geïmplementeerd in een web-app met de naam todolistangular, voert u 'https://todolistangular.azurewebsites.net' in.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-119">For example, if you deployed your JavaScript application to a web app named todolistangular, enter "https://todolistangular.azurewebsites.net".</span></span> <span data-ttu-id="ad0c0-120">Als alternatief kunt u een sterretje (*) invoeren als u wilt opgeven dat alle domeinen worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-120">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>


1. <span data-ttu-id="ad0c0-121">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-121">Click **Save**.</span></span>
   
   ![Op Opslaan klikken](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="ad0c0-123">Nadat u op **Opslaan** hebt geklikt, accepteert de API-app JavaScript-aanroepen vanuit de opgegeven URL's.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-123">After you click **Save**, the API app will accept JavaScript calls from the specified URLs.</span></span>

#### <a name="configure-cors-by-using-azure-resource-manager-tools"></a><span data-ttu-id="ad0c0-124">CORS configureren met de Azure Resource Manager-hulpprogramma's</span><span class="sxs-lookup"><span data-stu-id="ad0c0-124">Configure CORS by using Azure Resource Manager tools</span></span>
<span data-ttu-id="ad0c0-125">U kunt CORS ook configureren voor een API-app met behulp van [Azure Resource Manager-sjablonen](../azure-resource-manager/resource-group-authoring-templates.md) in opdrachtregelhulpprogramma's zoals [Azure PowerShell](/powershell/azureps-cmdlets-docs) en de [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ad0c0-125">You can also configure CORS for an API app by using [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) in command line tools such as [Azure PowerShell](/powershell/azureps-cmdlets-docs) and the [Azure CLI](../cli-install-nodejs.md).</span></span> 

<span data-ttu-id="ad0c0-126">Voor een voorbeeld van een Azure Resource Manager-sjabloon die de CORS-eigenschap instelt, opent u het [bestand azuredeploy.json in de opslagplaats voor de voorbeeldtoepassing uit deze zelfstudie](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="ad0c0-126">For an example of an Azure Resource Manager template that sets the CORS property, open the [azuredeploy.json file in the repository for this tutorial's sample application](https://github.com/azure-samples/app-service-api-dotnet-todo-list/blob/master/azuredeploy.json).</span></span> <span data-ttu-id="ad0c0-127">Ga naar het gedeelte van de sjabloon die lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ad0c0-127">Find the section of the template that looks like the following example:</span></span>

        "cors": {
            "allowedOrigins": [
                "todolistangular.azurewebsites.net"
            ]
        }

## <span data-ttu-id="ad0c0-128"><a id="tutorialstart"></a> Vervolg van de zelfstudie Aan de slag met .NET</span><span class="sxs-lookup"><span data-stu-id="ad0c0-128"><a id="tutorialstart"></a> Continuing the .NET getting-started tutorial</span></span>
<span data-ttu-id="ad0c0-129">Als u de reeks Aan de slag met Node.js of Java voor API-apps volgt, hebt u de Aan de slag-reeks nu voltooid.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-129">If you are following the Node.js or Java getting-started series for API apps, you have completed the getting started series.</span></span> <span data-ttu-id="ad0c0-130">Ga naar de sectie [Volgende stappen](#next-steps) voor suggesties voor meer informatiebronnen over API Apps.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-130">Skip to the [Next steps](#next-steps) section to find suggestions for further learning about API Apps.</span></span>

<span data-ttu-id="ad0c0-131">De rest van dit artikel is een vervolg van de reeks Aan de slag met .NET. Er wordt van uitgegaan dat u [de eerste zelfstudie](app-service-api-dotnet-get-started.md) met succes hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-131">The remainder of this article is a continuation of the .NET getting-started series and assumes that you successfully completed [the first tutorial](app-service-api-dotnet-get-started.md).</span></span>

## <a name="deploy-the-todolistangular-project-to-a-new-web-app"></a><span data-ttu-id="ad0c0-132">Het project ToDoListAngular implementeren in een nieuwe web-app</span><span class="sxs-lookup"><span data-stu-id="ad0c0-132">Deploy the ToDoListAngular project to a new web app</span></span>
<span data-ttu-id="ad0c0-133">In [de eerste zelfstudie](app-service-api-dotnet-get-started.md) hebt u een API-app voor de middelste laag en een API-app voor de gegevenslaag gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-133">In [the first tutorial](app-service-api-dotnet-get-started.md), you created a middle tier API app and a data tier API app.</span></span> <span data-ttu-id="ad0c0-134">In deze zelfstudie maakt u een SPA-web-app (SPA staat voor 'Single-Page Application') die de API-app voor de middelste laag aanroept.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-134">In this tutorial you create a single-page application (SPA) web app that calls the middle tier API app.</span></span> <span data-ttu-id="ad0c0-135">Voor de SPA moet u CORS inschakelen in de API-app voor de middelste laag.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-135">For the SPA to work you have to enable CORS on the middle tier API app.</span></span> 

<span data-ttu-id="ad0c0-136">In de [voorbeeldtoepassing ToDoList](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) is het project ToDoListAngular een eenvoudige AngularJS-client die het ToDoListAPI Web API-project voor de middelste laag aanroept.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-136">In the [ToDoList sample application](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list), the ToDoListAngular project is a simple AngularJS client that calls the middle tier ToDoListAPI Web API project.</span></span> <span data-ttu-id="ad0c0-137">De JavaScript-code in het bestand *app/scripts/todoListSvc.js* roept de API aan met behulp van de AngularJS HTTP-provider.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-137">The JavaScript code in the *app/scripts/todoListSvc.js* file calls the API by using the AngularJS HTTP provider.</span></span> 

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

### <a name="create-a-new-web-app-for-the-todolistangular-project"></a><span data-ttu-id="ad0c0-138">Een nieuwe web-app maken voor het project ToDoListAngular</span><span class="sxs-lookup"><span data-stu-id="ad0c0-138">Create a new web app for the ToDoListAngular project</span></span>
<span data-ttu-id="ad0c0-139">De procedure voor het maken van een nieuwe App Service-web-app en het vervolgens implementeren hiervan in een project is vergelijkbaar met wat u hebt gezien voor [het maken en implementeren van een API-app in de eerste zelfstudie van deze reeks](app-service-api-dotnet-get-started.md#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="ad0c0-139">The procedure to create a new App Service web app and deploy a project to it is similar to what you saw for [creating and deploying an API app in the first tutorial in this series](app-service-api-dotnet-get-started.md#createapiapp).</span></span> <span data-ttu-id="ad0c0-140">Het enige verschil is dat het type app **Web-app** is in plaats van **API-app**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-140">The only difference is that the app type is **Web App** instead of **API App**.</span></span>  <span data-ttu-id="ad0c0-141">Zie voor schermafbeeldingen van de dialoogvensters</span><span class="sxs-lookup"><span data-stu-id="ad0c0-141">For screen shots of the dialogs, see</span></span> 

1. <span data-ttu-id="ad0c0-142">Klik in **Solution Explorer** met de rechtermuisknop op het project ToDoListAngular. Klik vervolgens op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-142">In **Solution Explorer**, right-click the ToDoListAngular project, and then click **Publish**.</span></span>
2. <span data-ttu-id="ad0c0-143">Klik op het tabblad **Profile** van de wizard **Publish Web** op **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-143">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="ad0c0-144">Klik in het dialoogvenster **App Service** op **New**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-144">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="ad0c0-145">Voer op het tabblad **Hosting** van het dialoogvenster **Create App Service** in het veld **Web App Name** een naam in die uniek is in het domein *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-145">In the **Hosting** tab of the **Create App Service** dialog box, enter a **Web App Name** that is unique in the *azurewebsites.net* domain.</span></span> 
5. <span data-ttu-id="ad0c0-146">Kies in **Subscription** het Azure-abonnement waarmee u wilt werken.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-146">Choose the Azure **Subscription** you want to work with.</span></span>
6. <span data-ttu-id="ad0c0-147">Kies in de vervolgkeuzelijst **Resource Group** dezelfde resourcegroep die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-147">In the **Resource Group** drop-down list, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="ad0c0-148">Kies in de vervolgkeuzelijst **App Service Plan** hetzelfde abonnement dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-148">In the **App Service Plan** drop-down list, choose the same plan you created earlier.</span></span> 
8. <span data-ttu-id="ad0c0-149">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-149">Click **Create**.</span></span>
   
    <span data-ttu-id="ad0c0-150">Visual Studio maakt de web-app, maakt er een publicatieprofiel voor en geeft de stap **Connection** van de wizard **Publish Web** weer.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-150">Visual Studio creates the web app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
   
    <span data-ttu-id="ad0c0-151">Klik nog niet op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-151">Don't click **Publish** yet.</span></span> <span data-ttu-id="ad0c0-152">In de volgende sectie configureert u de nieuwe web-app om de API-app voor de middelste laag aan te roepen die wordt uitgevoerd in de App Service.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-152">In the following section, you configure the new web app to call the middle tier API app that is running in App Service.</span></span> 

### <a name="set-the-middle-tier-url-in-web-app-settings"></a><span data-ttu-id="ad0c0-153">De URL voor de middelste laag instellen in de instellingen voor web-apps</span><span class="sxs-lookup"><span data-stu-id="ad0c0-153">Set the middle tier URL in web app settings</span></span>
1. <span data-ttu-id="ad0c0-154">Ga naar de [Azure Portal](https://portal.azure.com/) en navigeer vervolgens naar de blade **Web-app** voor de web-app die u hebt gemaakt als host voor het (front-end-)project TodoListAngular.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-154">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **Web App** blade for the web app that you created to host the TodoListAngular (front end) project.</span></span>
2. <span data-ttu-id="ad0c0-155">Klik op **Instellingen > Toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-155">Click **Settings > Application Settings**.</span></span>
3. <span data-ttu-id="ad0c0-156">Geef in de sectie **App-instellingen** de volgende sleutel en waarde op:</span><span class="sxs-lookup"><span data-stu-id="ad0c0-156">In the **App settings** section, add the following key and value:</span></span>
   
   | <span data-ttu-id="ad0c0-157">Sleutel</span><span class="sxs-lookup"><span data-stu-id="ad0c0-157">Key</span></span> | <span data-ttu-id="ad0c0-158">Waarde</span><span class="sxs-lookup"><span data-stu-id="ad0c0-158">Value</span></span> | <span data-ttu-id="ad0c0-159">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="ad0c0-159">Example</span></span> |
   | --- | --- | --- |
   | <span data-ttu-id="ad0c0-160">toDoListAPIURL</span><span class="sxs-lookup"><span data-stu-id="ad0c0-160">toDoListAPIURL</span></span> |<span data-ttu-id="ad0c0-161">https://{de naam van uw API-app voor de middelste laag}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ad0c0-161">https://{your middle tier API app name}.azurewebsites.net</span></span> |<span data-ttu-id="ad0c0-162">https://todolistapi0121.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="ad0c0-162">https://todolistapi0121.azurewebsites.net</span></span> |
4. <span data-ttu-id="ad0c0-163">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-163">Click **Save**.</span></span>
   
    <span data-ttu-id="ad0c0-164">Wanneer de code in Azure wordt uitgevoerd, overschrijft deze waarde de localhost-URL die zich in het *Web.config*-bestand bevindt.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-164">When the code runs in Azure, this value overrides the localhost URL that is in the *Web.config* file.</span></span> 
   
    <span data-ttu-id="ad0c0-165">De code die de instellingswaarde krijgt, bevindt zich in *index.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="ad0c0-165">The code that gets the setting value is in *index.cshtml*:</span></span>
   
        <script type="text/javascript">
            var apiEndpoint = "@System.Configuration.ConfigurationManager.AppSettings["toDoListAPIURL"]";
        </script>
        <script src="app/scripts/todoListSvc.js"></script>
   
    <span data-ttu-id="ad0c0-166">De code in *todoListSvc.js* maakt gebruik van de instelling:</span><span class="sxs-lookup"><span data-stu-id="ad0c0-166">The code in *todoListSvc.js* uses the setting:</span></span>
   
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

### <a name="deploy-the-todolistangular-web-project-to-the-new-web-app"></a><span data-ttu-id="ad0c0-167">Het webproject ToDoListAngular implementeren in een nieuwe web-app</span><span class="sxs-lookup"><span data-stu-id="ad0c0-167">Deploy the ToDoListAngular web project to the new web app</span></span>
* <span data-ttu-id="ad0c0-168">Klik in Visual Studio in de stap **Connection** van de wizard **Publish Web** op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-168">In Visual Studio, in the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
  
   <span data-ttu-id="ad0c0-169">Visual Studio implementeert het project ToDoListAngular in de nieuwe web-app en opent een browservenster met de URL van de web-app.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-169">Visual Studio deploys the ToDoListAngular project to the new web app and opens a browser to the URL of the web app.</span></span> 

### <a name="test-the-application-without-cors-enabled"></a><span data-ttu-id="ad0c0-170">De toepassing testen zonder dat CORS is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="ad0c0-170">Test the application without CORS enabled</span></span>
1. <span data-ttu-id="ad0c0-171">Open in uw browser het consolevenster van de ontwikkelhulpprogramma’s.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-171">In your browser Developer Tools, open the Console window.</span></span>
2. <span data-ttu-id="ad0c0-172">Klik in het browservenster waarin de AngularJS-gebruikersinterface wordt weergegeven, op de koppeling **To Do List**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-172">In the browser window that displays the AngularJS UI, click the **To Do List** link.</span></span>
   
    <span data-ttu-id="ad0c0-173">De JavaScript-code probeert de API-app voor de middelste laag aan te roepen, maar de aanroep mislukt omdat de front-end in een ander domein wordt uitgevoerd dan de back-end.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-173">The JavaScript code tries to call the middle tier API app, but the call fails because the front end is running in a different domain than the back end.</span></span> <span data-ttu-id="ad0c0-174">In het consolevenster van de ontwikkelhulpprogramma’s van de browser wordt een cross-origin-foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-174">The browser's Developer Tools Console window shows a cross-origin error message.</span></span>
   
    ![Cross-origin-foutbericht](./media/app-service-api-cors-consume-javascript/consoleaccessdenied.png)

## <a name="configure-cors-for-the-middle-tier-api-app"></a><span data-ttu-id="ad0c0-176">CORS configureren voor de API-app voor de middelste laag</span><span class="sxs-lookup"><span data-stu-id="ad0c0-176">Configure CORS for the middle tier API app</span></span>
<span data-ttu-id="ad0c0-177">In deze sectie configureert u de CORS-instelling in Azure voor ToDoListAPI, de API-app voor de middelste laag.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-177">In this section, you configure the CORS setting in Azure for the middle tier ToDoListAPI API app.</span></span> <span data-ttu-id="ad0c0-178">Met deze instelling kan de API-app voor de middelste laag JavaScript-aanroepen ontvangen van de web-app die u hebt gemaakt voor het project ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-178">This setting will allow the middle tier API app to receive JavaScript calls from the web app that you created for the ToDoListAngular project.</span></span>

1. <span data-ttu-id="ad0c0-179">Ga in een browser naar de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ad0c0-179">In a browser, go to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ad0c0-180">Klik op **App Services** en vervolgens op de API-app ToDoListAPI (middelste laag).</span><span class="sxs-lookup"><span data-stu-id="ad0c0-180">Click **App Services**, and then click the ToDoListAPI (middle tier) API app.</span></span>
   
    ![De API-app in de portal selecteren](./media/app-service-api-cors-consume-javascript/browseapiapps.png)
3. <span data-ttu-id="ad0c0-182">Ga op de blade **Instellingen**, die rechts naast de blade **API-app** wordt geopend, naar de sectie **API** en klik vervolgens op **CORS**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-182">In the **Settings** blade that opens to the right of the **API app** blade, find the **API** section, and then click **CORS**.</span></span>
   
   ![CORS selecteren in de portal](./media/app-service-api-cors-consume-javascript/clicksettings.png)
4. <span data-ttu-id="ad0c0-184">Voer in het tekstvak de URL voor de web-app ToDoListAngular (front-end) in.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-184">In the text box, enter the URL for the ToDoListAngular (front end) web app.</span></span> <span data-ttu-id="ad0c0-185">Hebt u het project ToDoListAngular bijvoorbeeld geïmplementeerd voor een web-app met de naam todolistangular0121, dan staat u aanroepen toe van de URL `https://todolistangular0121.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-185">For example, if you deployed the ToDoListAngular project to a web app named todolistangular0121, allow calls from the URL `https://todolistangular0121.azurewebsites.net`.</span></span>
   
   <span data-ttu-id="ad0c0-186">Als alternatief kunt u een sterretje (*) invoeren als u wilt opgeven dat alle domeinen worden geaccepteerd.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-186">As an alternative, you can enter an asterisk (*) to specify that all origin domains are accepted.</span></span>
5. <span data-ttu-id="ad0c0-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-187">Click **Save**.</span></span>
   
   ![Op Opslaan klikken](./media/app-service-api-cors-consume-javascript/corsinportal.png)
   
   <span data-ttu-id="ad0c0-189">Nadat u op **Opslaan** hebt geklikt, accepteert de API-app JavaScript-aanroepen vanuit de opgegeven URL.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-189">After you click **Save**, the API app will accept JavaScript calls from the specified URL.</span></span> <span data-ttu-id="ad0c0-190">Op deze schermafbeelding accepteert de API-app ToDoListAPI0223 JavaScript-clientaanroepen van de web-app ToDoListAngular.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-190">In this screen shot, the ToDoListAPI0223 API app will accept JavaScript client calls from the ToDoListAngular web app.</span></span>

### <a name="test-the-application-with-cors-enabled"></a><span data-ttu-id="ad0c0-191">De toepassing testen met CORS ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="ad0c0-191">Test the application with CORS enabled</span></span>
* <span data-ttu-id="ad0c0-192">Open een browservenster met de HTTPS-URL van de web-app.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-192">Open a browser to the HTTPS URL of the web app.</span></span> 
  
    <span data-ttu-id="ad0c0-193">De toepassing staat u nu toe taken te bekijken, toe te voegen, te bewerken en te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-193">This time the application lets you view, add, edit, and delete to-do items.</span></span> 
  
    ![Takenlijstpagina van voorbeeld-app](./media/app-service-api-cors-consume-javascript/corssuccess.png)

## <a name="app-service-cors-versus-web-api-cors"></a><span data-ttu-id="ad0c0-195">App Service CORS versus Web API CORS</span><span class="sxs-lookup"><span data-stu-id="ad0c0-195">App Service CORS versus Web API CORS</span></span>
<span data-ttu-id="ad0c0-196">In een Web API-project kunt u het [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet-pakket installeren om in de code op te geven vanuit welke domeinen uw API JavaScript-aanroepen accepteert.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-196">In a Web API project, you can install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package to specify in code which domains your API will accept JavaScript calls from.</span></span>

<span data-ttu-id="ad0c0-197">Ondersteuning voor Web API CORS biedt meer flexibiliteit dan ondersteuning voor App Service CORS.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-197">Web API CORS support is more flexible than App Service CORS support.</span></span> <span data-ttu-id="ad0c0-198">Zo kunt u in de code voor verschillende actiemethoden verschillende toegestane bronnen opgeven. Voor App Service CORS kunt u voor alle methoden van uw API-app slechts één set toegestane bronnen opgeven.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-198">For example, in code you can specify different accepted origins for different action methods, while for App Service CORS you specify one set of accepted origins for all of an API app's methods.</span></span>

> [!NOTE]
> <span data-ttu-id="ad0c0-199">Gebruik Web API CORS en App Service CORS niet samen in één API-app.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-199">Don't try to use both Web API CORS and App Service CORS in one API app.</span></span> <span data-ttu-id="ad0c0-200">Doet u dit toch, dan krijgt App Service CORS voorrang en heeft Web API CORS geen effect.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-200">App Service CORS will take precedence and Web API CORS will have no effect.</span></span> <span data-ttu-id="ad0c0-201">Als u bijvoorbeeld in App Service één brondomein inschakelt en in uw Web API-code alle brondomeinen, accepteert uw Azure API-app alleen aanroepen van het domein dat u in Azure hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-201">For example, if you enable one origin domain in App Service, and enable all origin domains in your Web API code, your Azure API app will only accept calls from the domain you specified in Azure.</span></span>
> 
> 

### <a name="how-to-enable-cors-in-web-api-code"></a><span data-ttu-id="ad0c0-202">CORS inschakelen in de web API-code</span><span class="sxs-lookup"><span data-stu-id="ad0c0-202">How to enable CORS in Web API code</span></span>
<span data-ttu-id="ad0c0-203">De volgende stappen geven een overzicht van het proces voor het inschakelen van ondersteuning voor Web API CORS.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-203">The following steps summarize the process for enabling Web API CORS support.</span></span> <span data-ttu-id="ad0c0-204">Zie [Cross-origin-aanvragen inschakelen in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-204">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API 2](http://www.asp.net/web-api/overview/security/enabling-cross-origin-requests-in-web-api).</span></span>

1. <span data-ttu-id="ad0c0-205">Installeer in een Web API-project het [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-205">In a Web API project, install the [Microsoft.AspNet.WebApi.Cors](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Cors/) NuGet package.</span></span>
2. <span data-ttu-id="ad0c0-206">Voeg een `config.EnableCors()`coderegel in de **Register**-methode van de **WebApiConfig**-klasse toe, zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-206">Include a `config.EnableCors()` line of code in the **Register** method of the **WebApiConfig** class, as in the following example.</span></span> 
   
        public static class WebApiConfig
        {
            public static void Register(HttpConfiguration config)
            {
                // Web API configuration and services
   
                // The following line enables you to control CORS by using Web API code
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
3. <span data-ttu-id="ad0c0-207">Voeg in uw Web API-controller een `using`-instructie voor de `System.Web.Http.Cors`-naamruimte toe en voeg het `EnableCors`-kenmerk toe aan de controllerklasse of aan afzonderlijke actiemethoden.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-207">In your Web API controller, add a `using` statement for the `System.Web.Http.Cors` namespace, and add the `EnableCors` attribute to the controller class or to individual action methods.</span></span> <span data-ttu-id="ad0c0-208">In het volgende voorbeeld geldt CORS-ondersteuning voor de gehele controller.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-208">In the following example, CORS support applies to the entire controller.</span></span>
   
        namespace ToDoListAPI.Controllers 
        {
            [HttpOperationExceptionFilterAttribute]
            [EnableCors(origins:"https://todolistangular0121.azurewebsites.net", headers:"accept,content-type,origin,x-my-header", methods: "get,post")]
            public class ToDoListController : ApiController

## <a name="using-azure-api-management-with-api-apps"></a><span data-ttu-id="ad0c0-209">Azure API Management gebruiken met API-apps</span><span class="sxs-lookup"><span data-stu-id="ad0c0-209">Using Azure API Management with API Apps</span></span>
<span data-ttu-id="ad0c0-210">Als u Azure API Management met een API-app gebruikt, configureert u CORS in API Management in plaats van in de API-app.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-210">If you use Azure API Management with an API app, configure CORS in API Management instead of in the API app.</span></span> <span data-ttu-id="ad0c0-211">Zie de volgende bronnen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="ad0c0-211">For more information, see the following resources:</span></span>

* [<span data-ttu-id="ad0c0-212">Overzicht van Azure API Management (video: CORS begint bij 12:10)</span><span class="sxs-lookup"><span data-stu-id="ad0c0-212">Azure API Management Overview (video: CORS starts at 12:10)</span></span>](https://azure.microsoft.com/documentation/videos/azure-api-management-overview/)
* [<span data-ttu-id="ad0c0-213">API Management-beleid voor meerdere domeinen</span><span class="sxs-lookup"><span data-stu-id="ad0c0-213">API Management cross domain policies</span></span>](https://msdn.microsoft.com/library/azure/dn894084.aspx#CORS)

## <a name="troubleshooting"></a><span data-ttu-id="ad0c0-214">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="ad0c0-214">Troubleshooting</span></span>
<span data-ttu-id="ad0c0-215">Als u een probleem ervaart tijdens het doorlopen van deze zelfstudie, vindt hier u enkele ideeën voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-215">In case you run into a problem while going through this tutorial, here are some troubleshooting ideas.</span></span>

* <span data-ttu-id="ad0c0-216">Zorg ervoor dat u de nieuwste versie van de [Azure SDK voor .NET voor Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003) gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-216">Make sure that you're using the latest version of the [Azure SDK for .NET for Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="ad0c0-217">Zorg ervoor dat u `https` hebt ingevoerd in de CORS-instelling en dat u `https` gebruikt om de front-end web-app uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-217">Make sure that you entered `https` in the CORS setting, and make sure that you're using `https` to run the front-end web app.</span></span>
* <span data-ttu-id="ad0c0-218">Zorg ervoor dat u de CORS-instelling hebt ingevoerd in de API voor de middelste laag en niet in de front-end web-app.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-218">Make sure that you entered the CORS setting in the middle tier API app, not in the front-end web app.</span></span>
* <span data-ttu-id="ad0c0-219">Als u CORS zowel in de toepassingscode als in Azure App Service configureert, houd er dan rekening mee dat de App Service CORS-instelling overschrijft wat u in de toepassingscode doet.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-219">If you're configuring CORS in both application code and Azure App Service, note that the App Service CORS setting will override whatever you're doing in application code.</span></span> 

<span data-ttu-id="ad0c0-220">Zie [Problemen met Azure App Service-apps in Visual Studio oplossen](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md) voor meer informatie over de functies van Visual Studio die probleemoplossing vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-220">To learn more about Visual Studio features that simplify troubleshooting, see [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad0c0-221">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad0c0-221">Next steps</span></span>
<span data-ttu-id="ad0c0-222">In dit artikel hebt u gezien hoe u App Service CORS-ondersteuning kunt inschakelen, zodat client-JavaScript-code een API kan aanroepen in een ander domein.</span><span class="sxs-lookup"><span data-stu-id="ad0c0-222">In this article, you saw how to enable App Service CORS support so that client JavaScript code can call an API in a different domain.</span></span> <span data-ttu-id="ad0c0-223">Lees voor meer informatie over API-apps de [Kennismaking met verificatie in App Service](../app-service/app-service-authentication-overview.md) en ga vervolgens naar de zelfstudie [Gebruikersverificatie voor API-apps](app-service-api-dotnet-user-principal-auth.md).</span><span class="sxs-lookup"><span data-stu-id="ad0c0-223">To learn more about API apps, read the [introduction to authentication in App Service](../app-service/app-service-authentication-overview.md), and then go to the [user authentication for API apps](app-service-api-dotnet-user-principal-auth.md) tutorial.</span></span>


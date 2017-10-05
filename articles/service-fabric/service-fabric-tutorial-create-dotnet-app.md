---
title: Maak een .NET-toepassing voor Service Fabric | Microsoft Docs
description: Informatie over het maken van een toepassing met een front-ASP.NET Core en een stateful betrouwbare service back-end en de toepassing implementeren naar een cluster.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi, mikhegn
ms.openlocfilehash: ef50adf3af19bce494c3256308b443c8eaccdcea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="1f05d-103">Maken en implementeren van een toepassing met een front-ASP.NET Core Web API-service en een stateful back-endservice</span><span class="sxs-lookup"><span data-stu-id="1f05d-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="1f05d-104">Deze zelfstudie maakt deel uit een reeks.</span><span class="sxs-lookup"><span data-stu-id="1f05d-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="1f05d-105">U leert hoe een Azure Service Fabric-toepassing maken met een front-end van ASP.NET Core Web-API en een stateful back-end-service voor het opslaan van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="1f05d-105">You will learn how to create an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service to store your data.</span></span> <span data-ttu-id="1f05d-106">Wanneer u klaar bent, hebt u een stemtoepassing met een ASP.NET Core web-front-die stemmende resultaten worden opgeslagen in een stateful back-end-service in het cluster.</span><span class="sxs-lookup"><span data-stu-id="1f05d-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in the cluster.</span></span> <span data-ttu-id="1f05d-107">Als u niet wilt dat u handmatig de stemtoepassing maken, kunt u [download de broncode](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) voor de voltooide toepassing en gaat u verder met [doorlopen van de stemmende voorbeeldtoepassing](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="1f05d-107">If you don't want to manually create the voting application, you can [download the source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for the completed application and skip ahead to [Walk through the voting sample application](#walkthrough_anchor).</span></span>

![Diagram van de toepassing](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="1f05d-109">Deel een van de reeks, leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="1f05d-109">In part one of the series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f05d-110">Een ASP.NET Core Web API-service als betrouwbare stateful service maken</span><span class="sxs-lookup"><span data-stu-id="1f05d-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="1f05d-111">Een ASP.NET-webtoepassing Core-service als een stateless webservice maken</span><span class="sxs-lookup"><span data-stu-id="1f05d-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="1f05d-112">De omgekeerde proxy gebruiken om te communiceren met de stateful service</span><span class="sxs-lookup"><span data-stu-id="1f05d-112">Use the reverse proxy to communicate with the stateful service</span></span>

<span data-ttu-id="1f05d-113">In deze zelfstudie reeks leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="1f05d-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="1f05d-114">Een .NET-Service Fabric-toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="1f05d-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="1f05d-115">De toepassing naar een externe-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="1f05d-115">Deploy the application to a remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="1f05d-116">CI/CD met behulp van Visual Studio Team Services configureren</span><span class="sxs-lookup"><span data-stu-id="1f05d-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="1f05d-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1f05d-117">Prerequisites</span></span>
<span data-ttu-id="1f05d-118">Voordat u deze zelfstudie begint:</span><span class="sxs-lookup"><span data-stu-id="1f05d-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="1f05d-119">Als u geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="1f05d-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="1f05d-120">[Installeer Visual Studio 2017](https://www.visualstudio.com/) en installeer de **ontwikkelen van Azure** en **ASP.NET en web ontwikkeling** werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="1f05d-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install the **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="1f05d-121">De Service Fabric SDK installeren</span><span class="sxs-lookup"><span data-stu-id="1f05d-121">Install the Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="1f05d-122">Een ASP.NET Web API-service als een betrouwbare service maken</span><span class="sxs-lookup"><span data-stu-id="1f05d-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="1f05d-123">Maak eerst de web-front-van de stemmende toepassing met behulp van ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="1f05d-123">First, create the web front-end of the voting application using ASP.NET Core.</span></span> <span data-ttu-id="1f05d-124">ASP.NET Core is een lichtgewicht, platformoverschrijdende ontwikkeling webframework die u gebruiken kunt voor het maken van moderne webgebruikersinterface en web-API's.</span><span class="sxs-lookup"><span data-stu-id="1f05d-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use to create modern web UI and web APIs.</span></span> <span data-ttu-id="1f05d-125">Als u een compleet begrip van hoe ASP.NET Core met Service Fabric integreert, wordt aangeraden lezen via de [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1f05d-125">To get a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through the [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="1f05d-126">Op dit moment kunt u deze zelfstudie voor snel aan de slag.</span><span class="sxs-lookup"><span data-stu-id="1f05d-126">For now, you can follow this tutorial to get started quickly.</span></span> <span data-ttu-id="1f05d-127">Zie voor meer informatie over ASP.NET Core, de [ASP.NET Core documentatie](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="1f05d-127">To learn more about ASP.NET Core, see the [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="1f05d-128">Deze zelfstudie is gebaseerd op de [ASP.NET Core tools voor Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="1f05d-128">This tutorial is based on the [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="1f05d-129">De .NET Core hulpprogramma's voor Visual Studio 2015 worden niet langer bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1f05d-129">The .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="1f05d-130">Start Visual Studio als **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="1f05d-131">Maken van een project met **bestand**->**nieuw**->**Project**</span><span class="sxs-lookup"><span data-stu-id="1f05d-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="1f05d-132">Kies in het dialoogvenster **Nieuw Project** de optie **Cloud > Service Fabric-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-132">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="1f05d-133">Naam van de toepassing **Voting** en druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-133">Name the application **Voting** and press **OK**.</span></span>

   ![Dialoogvenster voor nieuw project in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="1f05d-135">Op de **nieuwe Service Fabric-Service** pagina **staatloze ASP.NET Core**, en de naam van uw service **VotingWeb**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-135">On the **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![ASP.NET-webservice te kiezen in het dialoogvenster voor nieuwe service](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="1f05d-137">De volgende pagina bevat een set van ASP.NET Core projectsjablonen.</span><span class="sxs-lookup"><span data-stu-id="1f05d-137">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="1f05d-138">Voor deze zelfstudie kiest **webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![ASP.NET-project kiezen](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="1f05d-140">Visual Studio maakt een toepassing en een serviceproject en geeft deze weer in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="1f05d-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![Solution Explorer na het maken van een toepassing met ASP.NET core Web API-service]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-to-the-votingweb-service"></a><span data-ttu-id="1f05d-142">AngularJS toevoegen aan de VotingWeb-service</span><span class="sxs-lookup"><span data-stu-id="1f05d-142">Add AngularJS to the VotingWeb service</span></span>
<span data-ttu-id="1f05d-143">Voeg [AngularJS](http://angularjs.org/) met uw service met de ingebouwde [Bower ondersteuning](/aspnet/core/client-side/bower).</span><span class="sxs-lookup"><span data-stu-id="1f05d-143">Add [AngularJS](http://angularjs.org/) to your service using the built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="1f05d-144">Open *bower.json* en vermeldingen voor hoeken en hoekvormige bootstrap toevoegen en vervolgens uw wijzigingen niet opslaan.</span><span class="sxs-lookup"><span data-stu-id="1f05d-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

```json
{
  "name": "asp.net",
  "private": true,
  "dependencies": {
    "bootstrap": "3.3.7",
    "jquery": "2.2.0",
    "jquery-validation": "1.14.0",
    "jquery-validation-unobtrusive": "3.2.6",
    "angular": "v1.6.5",
    "angular-bootstrap": "v1.1.0"
  }
}
```
<span data-ttu-id="1f05d-145">Bij het opslaan de *bower.json* bestand Angular is geïnstalleerd in uw project *wwwroot/lib* map.</span><span class="sxs-lookup"><span data-stu-id="1f05d-145">Upon saving the *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="1f05d-146">Bovendien wordt vermeld in de *afhankelijkheden/Bower* map.</span><span class="sxs-lookup"><span data-stu-id="1f05d-146">Additionally, it is listed within the *Dependencies/Bower* folder.</span></span>

### <a name="update-the-sitejs-file"></a><span data-ttu-id="1f05d-147">Het bestand site.js bijwerken</span><span class="sxs-lookup"><span data-stu-id="1f05d-147">Update the site.js file</span></span>
<span data-ttu-id="1f05d-148">Open de *wwwroot/js/site.js* bestand.</span><span class="sxs-lookup"><span data-stu-id="1f05d-148">Open the *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="1f05d-149">De inhoud ervan vervangen door JavaScript gebruikt door de startpagina weergaven:</span><span class="sxs-lookup"><span data-stu-id="1f05d-149">Replace its contents with the JavaScript used by the Home views:</span></span>

```javascript
var app = angular.module('VotingApp', ['ui.bootstrap']);
app.run(function () { });

app.controller('VotingAppController', ['$rootScope', '$scope', '$http', '$timeout', function ($rootScope, $scope, $http, $timeout) {

    $scope.refresh = function () {
        $http.get('api/Votes?c=' + new Date().getTime())
            .then(function (data, status) {
                $scope.votes = data;
            }, function (data, status) {
                $scope.votes = undefined;
            });
    };

    $scope.remove = function (item) {
        $http.delete('api/Votes/' + item)
            .then(function (data, status) {
                $scope.refresh();
            })
    };

    $scope.add = function (item) {
        var fd = new FormData();
        fd.append('item', item);
        $http.put('api/Votes/' + item, fd, {
            transformRequest: angular.identity,
            headers: { 'Content-Type': undefined }
        })
            .then(function (data, status) {
                $scope.refresh();
                $scope.item = undefined;
            })
    };
}]);
```

### <a name="update-the-indexcshtml-file"></a><span data-ttu-id="1f05d-150">Het bestand Index.cshtml bijwerken</span><span class="sxs-lookup"><span data-stu-id="1f05d-150">Update the Index.cshtml file</span></span>
<span data-ttu-id="1f05d-151">Open de *Views/Home/Index.cshtml* -bestand, de weergave die specifiek zijn voor de controller startpagina.</span><span class="sxs-lookup"><span data-stu-id="1f05d-151">Open the *Views/Home/Index.cshtml* file, the view specific to the Home controller.</span></span>  <span data-ttu-id="1f05d-152">Vervang de inhoud door het volgende, sla de wijzigingen vervolgens.</span><span class="sxs-lookup"><span data-stu-id="1f05d-152">Replace its contents with the following, then save your changes.</span></span>

```html
@{
    ViewData["Title"] = "Service Fabric Voting Sample";
}

<div ng-controller="VotingAppController" ng-init="refresh()">
    <div class="container-fluid">
        <div class="row">
            <div class="col-xs-8 col-xs-offset-2 text-center">
                <h2>Service Fabric Voting Sample</h2>
            </div>
        </div>

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <form class="col-xs-12 center-block">
                    <div class="col-xs-6 form-group">
                        <input id="txtAdd" type="text" class="form-control" placeholder="Add voting option" ng-model="item" />
                    </div>
                    <button id="btnAdd" class="btn btn-default" ng-click="add(item)">
                        <span class="glyphicon glyphicon-plus" aria-hidden="true"></span>
                        Add
                    </button>
                </form>
            </div>
        </div>

        <hr />

        <div class="row">
            <div class="col-xs-8 col-xs-offset-2">
                <div class="row">
                    <div class="col-xs-4">
                        Click to vote
                    </div>
                </div>
                <div class="row top-buffer" ng-repeat="vote in votes.data">
                    <div class="col-xs-8">
                        <button class="btn btn-success text-left btn-block" ng-click="add(vote.key)">
                            <span class="pull-left">
                                {{vote.key}}
                            </span>
                            <span class="badge pull-right">
                                {{vote.value}} Votes
                            </span>
                        </button>
                    </div>
                    <div class="col-xs-4">
                        <button class="btn btn-danger pull-right btn-block" ng-click="remove(vote.key)">
                            <span class="glyphicon glyphicon-remove" aria-hidden="true"></span>
                            Remove
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
```

### <a name="update-the-layoutcshtml-file"></a><span data-ttu-id="1f05d-153">Het bestand _Layout.cshtml bijwerken</span><span class="sxs-lookup"><span data-stu-id="1f05d-153">Update the _Layout.cshtml file</span></span>
<span data-ttu-id="1f05d-154">Open de *Views/Shared/_Layout.cshtml* -bestand, de standaardindeling voor de ASP.NET-app.</span><span class="sxs-lookup"><span data-stu-id="1f05d-154">Open the *Views/Shared/_Layout.cshtml* file, the default layout for the ASP.NET app.</span></span>  <span data-ttu-id="1f05d-155">Vervang de inhoud door het volgende, sla de wijzigingen vervolgens.</span><span class="sxs-lookup"><span data-stu-id="1f05d-155">Replace its contents with the following, then save your changes.</span></span>

```html
<!DOCTYPE html>
<html ng-app="VotingApp" xmlns:ng="http://angularjs.org">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"]</title>

    <link href="~/lib/bootstrap/dist/css/bootstrap.min.css" rel="stylesheet" />
    <link href="~/css/site.css" rel="stylesheet" />

</head>
<body>
    <div class="container body-content">
        @RenderBody()
    </div>

    <script src="~/lib/jquery/dist/jquery.js"></script>
    <script src="~/lib/bootstrap/dist/js/bootstrap.js"></script>
    <script src="~/lib/angular/angular.js"></script>
    <script src="~/lib/angular-bootstrap/ui-bootstrap-tpls.js"></script>
    <script src="~/js/site.js"></script>

    @RenderSection("Scripts", required: false)
</body>
</html>
```

### <a name="update-the-votingwebcs-file"></a><span data-ttu-id="1f05d-156">Het bestand VotingWeb.cs bijwerken</span><span class="sxs-lookup"><span data-stu-id="1f05d-156">Update the VotingWeb.cs file</span></span>
<span data-ttu-id="1f05d-157">Open de *VotingWeb.cs* bestand, dat wordt gemaakt van de WebHost ASP.NET Core binnen de staatloze service met de webserver WebListener.</span><span class="sxs-lookup"><span data-stu-id="1f05d-157">Open the *VotingWeb.cs* file, which creates the ASP.NET Core WebHost inside the stateless service using the WebListener web server.</span></span>  <span data-ttu-id="1f05d-158">Voeg de `using System.Net.Http;` richtlijn boven aan het bestand.</span><span class="sxs-lookup"><span data-stu-id="1f05d-158">Add the `using System.Net.Http;` directive to the top of the file.</span></span>  <span data-ttu-id="1f05d-159">Vervang de `CreateServiceInstanceListeners()` werken met het volgende en sla vervolgens uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="1f05d-159">Replace the `CreateServiceInstanceListeners()` function with the following, then save your changes.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
            {
                ServiceEventSource.Current.ServiceMessage(serviceContext, $"Starting WebListener on {url}");

                return new WebHostBuilder().UseWebListener()
                            .ConfigureServices(
                                services => services
                                    .AddSingleton<StatelessServiceContext>(serviceContext)
                                    .AddSingleton<HttpClient>())
                            .UseContentRoot(Directory.GetCurrentDirectory())
                            .UseStartup<Startup>()
                            .UseApplicationInsights()
                            .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                            .UseUrls(url)
                            .Build();
            }))
    };
}
```

### <a name="add-the-votescontrollercs-file"></a><span data-ttu-id="1f05d-160">Het bestand VotesController.cs toevoegen</span><span class="sxs-lookup"><span data-stu-id="1f05d-160">Add the VotesController.cs file</span></span>
<span data-ttu-id="1f05d-161">Een controller waarmee wordt gedefinieerd stemmende acties toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1f05d-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="1f05d-162">Met de rechtermuisknop op de **domeincontrollers** map, selecteer vervolgens **toevoegen -> Nieuw item -> klasse**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-162">Right-click on the **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="1f05d-163">Naam van het bestand 'VotesController.cs' en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-163">Name the file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="1f05d-164">Inhoud van het bestand vervangen door de volgende, sla de wijzigingen vervolgens.</span><span class="sxs-lookup"><span data-stu-id="1f05d-164">Replace the file contents with the following, then save your changes.</span></span>  <span data-ttu-id="1f05d-165">Verderop in [bijwerken van het bestand VotesController.cs](#updatevotecontroller_anchor), wordt dit bestand worden gewijzigd om te lezen en schrijven van stemmende gegevens op de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="1f05d-165">Later, in [Update the VotesController.cs file](#updatevotecontroller_anchor), this file will be modified to read and write voting data from the back-end service.</span></span>  <span data-ttu-id="1f05d-166">Op dit moment retourneert de controller statische tekenreeksgegevens naar de weergave.</span><span class="sxs-lookup"><span data-stu-id="1f05d-166">For now, the controller returns static string data to the view.</span></span>

```csharp
using System;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using System.Collections.Generic;
using Newtonsoft.Json;
using System.Text;
using System.Net.Http;
using System.Net.Http.Headers;

namespace VotingWeb.Controllers
{
    [Produces("application/json")]
    [Route("api/Votes")]
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            List<KeyValuePair<string, int>> votes= new List<KeyValuePair<string, int>>();
            votes.Add(new KeyValuePair<string, int>("Pizza", 3));
            votes.Add(new KeyValuePair<string, int>("Ice cream", 4));

            return Json(votes);
        }
     }
}
```



### <a name="deploy-and-run-the-application-locally"></a><span data-ttu-id="1f05d-167">Implementeren en de toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="1f05d-167">Deploy and run the application locally</span></span>
<span data-ttu-id="1f05d-168">U kunt nu doorgaan en de toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1f05d-168">You can now go ahead and run the application.</span></span> <span data-ttu-id="1f05d-169">Druk op `F5` in Visual Studio om de toepassing voor foutopsporing te implementeren.</span><span class="sxs-lookup"><span data-stu-id="1f05d-169">In Visual Studio, press `F5` to deploy the application for debugging.</span></span> <span data-ttu-id="1f05d-170">`F5`mislukt als u niet eerder Visual Studio als Open **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="1f05d-171">De eerste keer dat u de toepassing lokaal uitvoert en implementeert, wordt door Visual Studio een lokaal cluster voor foutopsporing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1f05d-171">The first time you run and deploy the application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="1f05d-172">Maken van het cluster kan enige tijd duren.</span><span class="sxs-lookup"><span data-stu-id="1f05d-172">Cluster creation may take some time.</span></span> <span data-ttu-id="1f05d-173">De status van het maken van het cluster wordt weergegeven in het Visual Studio-uitvoervenster.</span><span class="sxs-lookup"><span data-stu-id="1f05d-173">The cluster creation status is displayed in the Visual Studio output window.</span></span>

<span data-ttu-id="1f05d-174">Uw web-app moet er op dit punt wordt als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="1f05d-174">At this point, your web app should look like this:</span></span>

![ASP.NET Core front-](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="1f05d-176">Als u wilt stop de foutopsporing voor de toepassing, gaat u terug naar Visual Studio en druk op **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-176">To stop debugging the application, go back to Visual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-to-your-application"></a><span data-ttu-id="1f05d-177">Een stateful back-endservice toevoegt aan uw toepassing</span><span class="sxs-lookup"><span data-stu-id="1f05d-177">Add a stateful back-end service to your application</span></span>
<span data-ttu-id="1f05d-178">Nu dat we een ASP.NET Web API-service die in onze toepassing wordt uitgevoerd hebben, maar eens en een stateful betrouwbare service voor het opslaan van sommige gegevens in onze toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1f05d-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service to store some data in our application.</span></span>

<span data-ttu-id="1f05d-179">Service Fabric kunt u voor het opslaan van uw gegevens rechtstreeks in uw service met behulp van betrouwbare verzamelingen consistent en betrouwbaar.</span><span class="sxs-lookup"><span data-stu-id="1f05d-179">Service Fabric allows you to consistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="1f05d-180">Betrouwbare verzamelingen zijn een set van maximaal beschikbare en betrouwbare verzameling klassen die bekend zijn voor iedereen die is gebruikt C#-verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="1f05d-180">Reliable collections are a set of highly available and reliable collection classes that are familiar to anyone who has used C# collections.</span></span>

<span data-ttu-id="1f05d-181">In deze zelfstudie maakt u een service die een itemwaarde in een betrouwbare verzameling opslaat.</span><span class="sxs-lookup"><span data-stu-id="1f05d-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="1f05d-182">Klik in Solution Explorer met de rechtermuisknop op **Services** in de toepassing project en kies **toevoegen > nieuwe Service Fabric-Service**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-182">In Solution Explorer, right-click **Services** within the application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Een nieuwe service toe te voegen aan een bestaande toepassing](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="1f05d-184">In de **nieuwe Service Fabric-Service** dialoogvenster kiezen **Stateful ASP.NET Core**, en de naam van de service **VotingData** en druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-184">In the **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name the service **VotingData** and press **OK**.</span></span>

    ![Dialoogvenster voor nieuwe service in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="1f05d-186">Nadat uw serviceproject is gemaakt, hebt u twee services in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="1f05d-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="1f05d-187">Als u doorgaat met uw toepassing bouwen, kunt u meer services die zich op dezelfde manier kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1f05d-187">As you continue to build your application, you can add more services in the same way.</span></span> <span data-ttu-id="1f05d-188">Elk zijn onafhankelijk samengestelde en bijgewerkte.</span><span class="sxs-lookup"><span data-stu-id="1f05d-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="1f05d-189">De volgende pagina bevat een set van ASP.NET Core projectsjablonen.</span><span class="sxs-lookup"><span data-stu-id="1f05d-189">The next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="1f05d-190">Voor deze zelfstudie kiest **Web API**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-190">For this tutorial, choose **Web API**.</span></span>

    ![ASP.NET-project kiezen](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="1f05d-192">Visual Studio maakt een serviceproject en geeft deze weer in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="1f05d-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Solution Explorer](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-the-votedatacontrollercs-file"></a><span data-ttu-id="1f05d-194">Het bestand VoteDataController.cs toevoegen</span><span class="sxs-lookup"><span data-stu-id="1f05d-194">Add the VoteDataController.cs file</span></span>

<span data-ttu-id="1f05d-195">In de **VotingData** project met de rechtermuisknop op de **domeincontrollers** map, selecteer vervolgens **toevoegen -> Nieuw item -> klasse**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-195">In the **VotingData** project right-click on the **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="1f05d-196">Naam van het bestand 'VoteDataController.cs' en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-196">Name the file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="1f05d-197">Inhoud van het bestand vervangen door de volgende, sla de wijzigingen vervolgens.</span><span class="sxs-lookup"><span data-stu-id="1f05d-197">Replace the file contents with the following, then save your changes.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;
using Microsoft.ServiceFabric.Data;
using System.Threading;
using Microsoft.ServiceFabric.Data.Collections;

namespace VotingData.Controllers
{
    [Route("api/[controller]")]
    public class VoteDataController : Controller
    {
        private readonly IReliableStateManager stateManager;

        public VoteDataController(IReliableStateManager stateManager)
        {
            this.stateManager = stateManager;
        }

        // GET api/VoteData
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            var ct = new CancellationToken();

            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                var list = await votesDictionary.CreateEnumerableAsync(tx);

                var enumerator = list.GetAsyncEnumerator();

                var result = new List<KeyValuePair<string, int>>();

                while (await enumerator.MoveNextAsync(ct))
                {
                    result.Add(enumerator.Current);
                }

                return Json(result);
            }
        }

        // PUT api/VoteData/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                await votesDictionary.AddOrUpdateAsync(tx, name, 1, (key, oldvalue) => oldvalue + 1);
                await tx.CommitAsync();
            }

            return new OkResult();
        }

        // DELETE api/VoteData/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            var votesDictionary = await this.stateManager.GetOrAddAsync<IReliableDictionary<string, int>>("counts");

            using (ITransaction tx = this.stateManager.CreateTransaction())
            {
                if (await votesDictionary.ContainsKeyAsync(tx, name))
                {
                    await votesDictionary.TryRemoveAsync(tx, name);
                    await tx.CommitAsync();
                    return new OkResult();
                }
                else
                {
                    return new NotFoundResult();
                }
            }
        }
    }
}
```


## <a name="connect-the-services"></a><span data-ttu-id="1f05d-198">Verbinding maken met de services</span><span class="sxs-lookup"><span data-stu-id="1f05d-198">Connect the services</span></span>
<span data-ttu-id="1f05d-199">In deze stap, wordt er verbinding maken met de twee services en de front-end-webservers toepassing get en set-informatie van de back-endservice stemmen.</span><span class="sxs-lookup"><span data-stu-id="1f05d-199">In this next step, we will connect the two services and make the front-end Web application get and set voting information from the back-end service.</span></span>

<span data-ttu-id="1f05d-200">Service Fabric biedt volledige flexibiliteit in hoe u met reliable services communiceren.</span><span class="sxs-lookup"><span data-stu-id="1f05d-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="1f05d-201">Binnen één toepassing hebt u mogelijk services die toegankelijk via TCP zijn.</span><span class="sxs-lookup"><span data-stu-id="1f05d-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="1f05d-202">Andere services die mogelijk toegankelijk via een HTTP REST-API en nog andere services kunnen toegang worden verkregen via websockets.</span><span class="sxs-lookup"><span data-stu-id="1f05d-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="1f05d-203">Zie voor achtergrondinformatie over de beschikbare opties en de wisselwerking betrokken [services communiceert](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="1f05d-203">For background on the options available and the tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="1f05d-204">In deze zelfstudie gebruiken we [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="1f05d-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-the-votescontrollercs-file"></a><span data-ttu-id="1f05d-205">Het bestand VotesController.cs bijwerken</span><span class="sxs-lookup"><span data-stu-id="1f05d-205">Update the VotesController.cs file</span></span>
<span data-ttu-id="1f05d-206">In de **VotingWeb** project, open de *Controllers/VotesController.cs* bestand.</span><span class="sxs-lookup"><span data-stu-id="1f05d-206">In the **VotingWeb** project, open the *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="1f05d-207">Vervang de `VotesController` definitie inhoud met de volgende klasse en sla vervolgens uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="1f05d-207">Replace the `VotesController` class definition contents with the following, then save your changes.</span></span>

```csharp
    public class VotesController : Controller
    {
        private readonly HttpClient httpClient;
        string serviceProxyUrl = "http://localhost:19081/Voting/VotingData/api/VoteData";
        string partitionKind = "Int64Range";
        string partitionKey = "0";

        public VotesController(HttpClient httpClient)
        {
            this.httpClient = httpClient;
        }

        // GET: api/Votes
        [HttpGet]
        public async Task<IActionResult> Get()
        {
            IEnumerable<KeyValuePair<string, int>> votes;

            HttpResponseMessage response = await this.httpClient.GetAsync($"{serviceProxyUrl}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            votes = JsonConvert.DeserializeObject<List<KeyValuePair<string, int>>>(await response.Content.ReadAsStringAsync());

            return Json(votes);
        }

        // PUT: api/Votes/name
        [HttpPut("{name}")]
        public async Task<IActionResult> Put(string name)
        {
            string payload = $"{{ 'name' : '{name}' }}";
            StringContent putContent = new StringContent(payload, Encoding.UTF8, "application/json");
            putContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");

            string proxyUrl = $"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}";

            HttpResponseMessage response = await this.httpClient.PutAsync(proxyUrl, putContent);

            return new ContentResult()
            {
                StatusCode = (int)response.StatusCode,
                Content = await response.Content.ReadAsStringAsync()
            };
        }

        // DELETE: api/Votes/name
        [HttpDelete("{name}")]
        public async Task<IActionResult> Delete(string name)
        {
            HttpResponseMessage response = await this.httpClient.DeleteAsync($"{serviceProxyUrl}/{name}?PartitionKind={partitionKind}&PartitionKey={partitionKey}");

            if (response.StatusCode != System.Net.HttpStatusCode.OK)
            {
                return this.StatusCode((int)response.StatusCode);
            }

            return new OkResult();

        }
    }
```
<a id="walkthrough" name="walkthrough_anchor"></a>

## <a name="walk-through-the-voting-sample-application"></a><span data-ttu-id="1f05d-208">Doorloop de stemmende voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="1f05d-208">Walk through the voting sample application</span></span>
<span data-ttu-id="1f05d-209">De stemtoepassing bestaat uit twee services:</span><span class="sxs-lookup"><span data-stu-id="1f05d-209">The voting application consists of two services:</span></span>
- <span data-ttu-id="1f05d-210">Web-front-service (VotingWeb): een ASP.NET Core web-front-service, die de webpagina fungeert en zichtbaar gemaakt web-API's om te communiceren met de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="1f05d-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves the web page and exposes web APIs to communicate with the backend service.</span></span>
- <span data-ttu-id="1f05d-211">Back-end-service (VotingData)-Core van een ASP.NET-webservice, die wordt er een API voor het opslaan van de stem resultaten in een betrouwbare woordenlijst persistent op schijf.</span><span class="sxs-lookup"><span data-stu-id="1f05d-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API to store the vote results in a reliable dictionary persisted on disk.</span></span>

![Diagram van de toepassing](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="1f05d-213">Wanneer u in de toepassing stemmen gebeurt het volgende:</span><span class="sxs-lookup"><span data-stu-id="1f05d-213">When you vote in the application the following events occur:</span></span>
1. <span data-ttu-id="1f05d-214">Een JavaScript verzendt de stemaanvraag naar de web-API in de web-front-endservice als een HTTP PUT-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="1f05d-214">A JavaScript sends the vote request to the web API in the web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="1f05d-215">De web-front-service wordt een proxyserver gebruikt om te zoeken en doorsturen van een HTTP PUT-aanvraag naar de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="1f05d-215">The web front-end service uses a proxy to locate and forward an HTTP PUT request to the back-end service.</span></span>

3. <span data-ttu-id="1f05d-216">De back-endservice nodig van de binnenkomende aanvraag en slaat de bijgewerkte resultaten in een betrouwbare woordenlijst die wordt gerepliceerd naar meerdere knooppunten binnen het cluster en opgeslagen op schijf.</span><span class="sxs-lookup"><span data-stu-id="1f05d-216">The back-end service takes the incoming request, and stores the updated result in a reliable dictionary, which gets replicated to multiple nodes within the cluster and persisted on disk.</span></span> <span data-ttu-id="1f05d-217">Gegevens van de toepassing wordt opgeslagen in het cluster, zodat er geen database nodig is.</span><span class="sxs-lookup"><span data-stu-id="1f05d-217">All the application's data is stored in the cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="1f05d-218">Fouten opsporen in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f05d-218">Debug in Visual Studio</span></span>
<span data-ttu-id="1f05d-219">Als u fouten opspoort toepassing in Visual Studio, gebruikt u een lokaal cluster van de Service Fabric-ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="1f05d-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="1f05d-220">U hebt de optie voor het aanpassen van uw ervaring foutopsporing op uw scenario.</span><span class="sxs-lookup"><span data-stu-id="1f05d-220">You have the option to adjust your debugging experience to your scenario.</span></span> <span data-ttu-id="1f05d-221">In deze toepassing opgeslagen gegevens in onze back-end-service met behulp van een betrouwbare woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="1f05d-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="1f05d-222">Visual Studio verwijdert u de toepassing per standaard, wanneer u het foutopsporingsprogramma stopt.</span><span class="sxs-lookup"><span data-stu-id="1f05d-222">Visual Studio removes the application per default when you stop the debugger.</span></span> <span data-ttu-id="1f05d-223">De toepassing is verwijderd, worden de gegevens in de back-end-service ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1f05d-223">Removing the application causes the data in the back-end service to also be removed.</span></span> <span data-ttu-id="1f05d-224">Om te blijven behouden de gegevens tussen foutopsporingssessies, kunt u de **toepassing foutopsporingsmodus** als eigenschap op de **Voting** -project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1f05d-224">To persist the data between debugging sessions, you can change the **Application Debug Mode** as a property on the **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="1f05d-225">Als u wilt kijken wat er in de code gebeurt, kunt u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1f05d-225">To look at what happens in the code, complete the following steps:</span></span>
1. <span data-ttu-id="1f05d-226">Open de **VotesController.cs** bestands- en stel een onderbrekingspunt in de web-API's **plaatsen** methode (regel 47) - u kunt zoeken naar het bestand in Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1f05d-226">Open the **VotesController.cs** file and set a breakpoint in the web API's **Put** method (line 47) - You can search for the file in the Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="1f05d-227">Open de **VoteDataController.cs** bestands- en stel een onderbrekingspunt in deze web-API **plaatsen** methode (line 50).</span><span class="sxs-lookup"><span data-stu-id="1f05d-227">Open the **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="1f05d-228">Ga terug naar de browser en klik op een optie of een nieuwe stemmende optie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1f05d-228">Go back to the browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="1f05d-229">U onderbrekingspunt de eerste in de web front-end van api-controller.</span><span class="sxs-lookup"><span data-stu-id="1f05d-229">You hit the first breakpoint in the web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="1f05d-230">Dit is waar de JavaScript in de browser wordt een aanvraag verzonden naar de web-API-controller in de front-end-service.</span><span class="sxs-lookup"><span data-stu-id="1f05d-230">This is where the JavaScript in the browser sends a request to the web API controller in the front-end service.</span></span>
    
    ![Stem front-end-Service toevoegen](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="1f05d-232">Eerst wordt de URL van de ReverseProxy opstellen voor onze back-endservice **(1)**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-232">First we construct the URL to the ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="1f05d-233">Vervolgens wordt de HTTP PUT-aanvraag naar de ReverseProxy verzenden **(2)**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-233">Then we send the HTTP PUT Request to the ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="1f05d-234">Ten slotte de we het antwoord van de back-end-service naar de client geretourneerd **(3)**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-234">Finally the we return the response from the back-end service to the client **(3)**.</span></span>

4. <span data-ttu-id="1f05d-235">Druk op **F5** om door te gaan</span><span class="sxs-lookup"><span data-stu-id="1f05d-235">Press **F5** to continue</span></span>
    1. <span data-ttu-id="1f05d-236">U bent nu op het punt onderbreking in de back-endservice.</span><span class="sxs-lookup"><span data-stu-id="1f05d-236">You are now at the break point in the back-end service.</span></span>
    
    ![Stem Back-End-Service toevoegen](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="1f05d-238">In de eerste regel in de methode **(1)** gebruiken we de `StateManager` ophalen of het toevoegen van een betrouwbare woordenlijst aangeroepen `counts`.</span><span class="sxs-lookup"><span data-stu-id="1f05d-238">In the first line in the method **(1)** we are using the `StateManager` to get or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="1f05d-239">Alle interacties met waarden in een betrouwbare woordenlijst vereisen een transactie, deze met de instructie **(2)** die transactie maakt.</span><span class="sxs-lookup"><span data-stu-id="1f05d-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="1f05d-240">In de transactie we vervolgens de waarde van de relevante sleutel voor de optie bijwerken en voert de bewerking **(3)**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-240">In the transaction, we then update the value of the relevant key for the voting option and commits the operation **(3)**.</span></span> <span data-ttu-id="1f05d-241">Als de gegevens van de commit-methode retourneert is bijgewerkt in de woordenlijst en gerepliceerd naar andere knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="1f05d-241">Once the commit method returns, the data is updated in the dictionary and replicated to other nodes in the cluster.</span></span> <span data-ttu-id="1f05d-242">De gegevens worden nu veilig opgeslagen in het cluster en de back-endservice failover naar andere knooppunten, nog steeds de gegevens beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="1f05d-242">The data is now safely stored in the cluster, and the back-end service can fail over to other nodes, still having the data available.</span></span>
5. <span data-ttu-id="1f05d-243">Druk op **F5** om door te gaan</span><span class="sxs-lookup"><span data-stu-id="1f05d-243">Press **F5** to continue</span></span>

<span data-ttu-id="1f05d-244">Als u wilt de Foutopsporingssessie stoppen, drukt u op **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="1f05d-244">To stop the debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1f05d-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f05d-245">Next steps</span></span>
<span data-ttu-id="1f05d-246">In dit deel van de zelfstudie hebt u geleerd hoe:</span><span class="sxs-lookup"><span data-stu-id="1f05d-246">In this part of the tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f05d-247">Een ASP.NET Core Web API-service als betrouwbare stateful service maken</span><span class="sxs-lookup"><span data-stu-id="1f05d-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="1f05d-248">Een ASP.NET-webtoepassing Core-service als een stateless webservice maken</span><span class="sxs-lookup"><span data-stu-id="1f05d-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="1f05d-249">De omgekeerde proxy gebruiken om te communiceren met de stateful service</span><span class="sxs-lookup"><span data-stu-id="1f05d-249">Use the reverse proxy to communicate with the stateful service</span></span>

<span data-ttu-id="1f05d-250">Ga naar de volgende zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="1f05d-250">Advance to the next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1f05d-251">De toepassing implementeren naar Azure</span><span class="sxs-lookup"><span data-stu-id="1f05d-251">Deploy the application to Azure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
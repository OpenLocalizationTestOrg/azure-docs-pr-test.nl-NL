---
title: een .NET-toepassing voor Service Fabric aaaCreate | Microsoft Docs
description: Ontdek hoe toocreate een toepassing met een front-ASP.NET Core en een betrouwbare stateful back-end-service en Hallo toepassing tooa cluster implementeren.
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
ms.openlocfilehash: bab331b9f8616c50a2794b6c048aace15579c8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a><span data-ttu-id="de964-103">Maken en implementeren van een toepassing met een front-ASP.NET Core Web API-service en een stateful back-endservice</span><span class="sxs-lookup"><span data-stu-id="de964-103">Create and deploy an application with an ASP.NET Core Web API front-end service and a stateful back-end service</span></span>
<span data-ttu-id="de964-104">Deze zelfstudie maakt deel uit een reeks.</span><span class="sxs-lookup"><span data-stu-id="de964-104">This tutorial is part one of a series.</span></span>  <span data-ttu-id="de964-105">U leert hoe toocreate een Azure Service Fabric-toepassing met een Web-API van ASP.NET Core front end en een stateful back-endservice toostore uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="de964-105">You will learn how toocreate an Azure Service Fabric application with an ASP.NET Core Web API front end and a stateful back-end service toostore your data.</span></span> <span data-ttu-id="de964-106">Wanneer u klaar bent, hebt u een stemtoepassing met een ASP.NET Core web-front-die stemmende resultaten worden opgeslagen in een stateful back-end-service in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="de964-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span> <span data-ttu-id="de964-107">Als u niet wilt dat toomanually Hallo stemmen toepassing maken, kunt u [Hallo broncode downloaden](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) voor Hallo voltooid toepassing en gaat u verder te[doorlopen Hallo stemmen voorbeeldtoepassing](#walkthrough_anchor).</span><span class="sxs-lookup"><span data-stu-id="de964-107">If you don't want toomanually create hello voting application, you can [download hello source code](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) for hello completed application and skip ahead too[Walk through hello voting sample application](#walkthrough_anchor).</span></span>

![Diagram van de toepassing](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="de964-109">Deel een reeks hello, leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="de964-109">In part one of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="de964-110">Een ASP.NET Core Web API-service als betrouwbare stateful service maken</span><span class="sxs-lookup"><span data-stu-id="de964-110">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="de964-111">Een ASP.NET-webtoepassing Core-service als een stateless webservice maken</span><span class="sxs-lookup"><span data-stu-id="de964-111">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="de964-112">Hallo omgekeerde proxy toocommunicate Hallo stateful service gebruiken</span><span class="sxs-lookup"><span data-stu-id="de964-112">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="de964-113">In deze zelfstudie reeks leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="de964-113">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="de964-114">Een .NET-Service Fabric-toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="de964-114">Build a .NET Service Fabric application</span></span>
> * [<span data-ttu-id="de964-115">Hallo toepassing tooa RAS-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="de964-115">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [<span data-ttu-id="de964-116">CI/CD met behulp van Visual Studio Team Services configureren</span><span class="sxs-lookup"><span data-stu-id="de964-116">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="de964-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="de964-117">Prerequisites</span></span>
<span data-ttu-id="de964-118">Voordat u deze zelfstudie begint:</span><span class="sxs-lookup"><span data-stu-id="de964-118">Before you begin this tutorial:</span></span>
- <span data-ttu-id="de964-119">Als u geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="de964-119">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="de964-120">[Installeer Visual Studio 2017](https://www.visualstudio.com/) en installeer Hallo **ontwikkelen van Azure** en **ASP.NET en web ontwikkeling** werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="de964-120">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="de964-121">Hallo Service Fabric SDK installeren</span><span class="sxs-lookup"><span data-stu-id="de964-121">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a><span data-ttu-id="de964-122">Een ASP.NET Web API-service als een betrouwbare service maken</span><span class="sxs-lookup"><span data-stu-id="de964-122">Create an ASP.NET Web API service as a reliable service</span></span>
<span data-ttu-id="de964-123">Maak eerst Hallo web front-Hallo stemmen toepassing via ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="de964-123">First, create hello web front-end of hello voting application using ASP.NET Core.</span></span> <span data-ttu-id="de964-124">ASP.NET Core is een lichtgewicht, platformoverschrijdende ontwikkeling webframework toocreate moderne webgebruikersinterface gebruiken en web-API's.</span><span class="sxs-lookup"><span data-stu-id="de964-124">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> <span data-ttu-id="de964-125">een volledig begrip van hoe ASP.NET Core met Service Fabric integreert tooget, wordt aangeraden lezen via Hallo [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="de964-125">tooget a complete understanding of how ASP.NET Core integrates with Service Fabric, we strongly recommend reading through hello [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) article.</span></span> <span data-ttu-id="de964-126">Op dit moment kunt u deze zelfstudie tooget snel aan de slag.</span><span class="sxs-lookup"><span data-stu-id="de964-126">For now, you can follow this tutorial tooget started quickly.</span></span> <span data-ttu-id="de964-127">toolearn meer informatie over ASP.NET Core, Zie Hallo [ASP.NET Core documentatie](https://docs.microsoft.com/aspnet/core/).</span><span class="sxs-lookup"><span data-stu-id="de964-127">toolearn more about ASP.NET Core, see hello [ASP.NET Core Documentation](https://docs.microsoft.com/aspnet/core/).</span></span>

> [!NOTE]
> <span data-ttu-id="de964-128">Deze zelfstudie is gebaseerd op Hallo [ASP.NET Core tools voor Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span><span class="sxs-lookup"><span data-stu-id="de964-128">This tutorial is based on hello [ASP.NET Core tools for Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc).</span></span> <span data-ttu-id="de964-129">Hallo .NET Core tools voor Visual Studio 2015 worden niet langer bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="de964-129">hello .NET Core tools for Visual Studio 2015 are no longer being updated.</span></span>

1. <span data-ttu-id="de964-130">Start Visual Studio als **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="de964-130">Launch Visual Studio as an **administrator**.</span></span>

2. <span data-ttu-id="de964-131">Maken van een project met **bestand**->**nieuw**->**Project**</span><span class="sxs-lookup"><span data-stu-id="de964-131">Create a project with **File**->**New**->**Project**</span></span>

3. <span data-ttu-id="de964-132">In Hallo **nieuw Project** dialoogvenster kiezen **Cloud > Service Fabric-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="de964-132">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

4. <span data-ttu-id="de964-133">Naam van de toepassing hello **Voting** en druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="de964-133">Name hello application **Voting** and press **OK**.</span></span>

   ![Dialoogvenster voor nieuw project in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. <span data-ttu-id="de964-135">Op Hallo **nieuwe Service Fabric-Service** pagina **staatloze ASP.NET Core**, en de naam van uw service **VotingWeb**.</span><span class="sxs-lookup"><span data-stu-id="de964-135">On hello **New Service Fabric Service** page, choose **Stateless ASP.NET Core**, and name your service **VotingWeb**.</span></span>
   
   ![ASP.NET-webservice te kiezen in het dialoogvenster voor nieuwe service Hallo](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. <span data-ttu-id="de964-137">de volgende pagina Hallo biedt een set van ASP.NET Core projectsjablonen.</span><span class="sxs-lookup"><span data-stu-id="de964-137">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="de964-138">Voor deze zelfstudie kiest **webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="de964-138">For this tutorial, choose **Web Application**.</span></span> 
   
   ![ASP.NET-project kiezen](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   <span data-ttu-id="de964-140">Visual Studio maakt een toepassing en een serviceproject en geeft deze weer in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="de964-140">Visual Studio creates an application and a service project and displays them in Solution Explorer.</span></span>

   ![Solution Explorer na het maken van een toepassing met ASP.NET core Web API-service]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a><span data-ttu-id="de964-142">AngularJS toohello VotingWeb service toevoegen</span><span class="sxs-lookup"><span data-stu-id="de964-142">Add AngularJS toohello VotingWeb service</span></span>
<span data-ttu-id="de964-143">Voeg [AngularJS](http://angularjs.org/) tooyour service met behulp van de ingebouwde Hallo [Bower ondersteuning](/aspnet/core/client-side/bower).</span><span class="sxs-lookup"><span data-stu-id="de964-143">Add [AngularJS](http://angularjs.org/) tooyour service using hello built-in [Bower support](/aspnet/core/client-side/bower).</span></span> <span data-ttu-id="de964-144">Open *bower.json* en vermeldingen voor hoeken en hoekvormige bootstrap toevoegen en vervolgens uw wijzigingen niet opslaan.</span><span class="sxs-lookup"><span data-stu-id="de964-144">Open *bower.json* and add entries for angular and angular-bootstrap, then save your changes.</span></span>

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
<span data-ttu-id="de964-145">Bij het opslaan van Hallo *bower.json* bestand Angular is geïnstalleerd in uw project *wwwroot/lib* map.</span><span class="sxs-lookup"><span data-stu-id="de964-145">Upon saving hello *bower.json* file, Angular is installed in your project's *wwwroot/lib* folder.</span></span> <span data-ttu-id="de964-146">Bovendien wordt vermeld in Hallo *afhankelijkheden/Bower* map.</span><span class="sxs-lookup"><span data-stu-id="de964-146">Additionally, it is listed within hello *Dependencies/Bower* folder.</span></span>

### <a name="update-hello-sitejs-file"></a><span data-ttu-id="de964-147">Hallo site.js bestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="de964-147">Update hello site.js file</span></span>
<span data-ttu-id="de964-148">Open Hallo *wwwroot/js/site.js* bestand.</span><span class="sxs-lookup"><span data-stu-id="de964-148">Open hello *wwwroot/js/site.js* file.</span></span>  <span data-ttu-id="de964-149">De inhoud ervan vervangen door Hallo JavaScript gebruikt door Hallo Home weergaven:</span><span class="sxs-lookup"><span data-stu-id="de964-149">Replace its contents with hello JavaScript used by hello Home views:</span></span>

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

### <a name="update-hello-indexcshtml-file"></a><span data-ttu-id="de964-150">Hallo Index.cshtml bestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="de964-150">Update hello Index.cshtml file</span></span>
<span data-ttu-id="de964-151">Open Hallo *Views/Home/Index.cshtml* bestand, Hallo specifieke toohello Home weergavebesturing.</span><span class="sxs-lookup"><span data-stu-id="de964-151">Open hello *Views/Home/Index.cshtml* file, hello view specific toohello Home controller.</span></span>  <span data-ttu-id="de964-152">Vervang de inhoud door de volgende Hallo en vervolgens uw wijzigingen niet opslaan.</span><span class="sxs-lookup"><span data-stu-id="de964-152">Replace its contents with hello following, then save your changes.</span></span>

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
                        Click toovote
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

### <a name="update-hello-layoutcshtml-file"></a><span data-ttu-id="de964-153">Hallo _Layout.cshtml bestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="de964-153">Update hello _Layout.cshtml file</span></span>
<span data-ttu-id="de964-154">Open Hallo *Views/Shared/_Layout.cshtml* bestand, Hallo standaardindeling voor Hallo ASP.NET-app.</span><span class="sxs-lookup"><span data-stu-id="de964-154">Open hello *Views/Shared/_Layout.cshtml* file, hello default layout for hello ASP.NET app.</span></span>  <span data-ttu-id="de964-155">Vervang de inhoud door de volgende Hallo en vervolgens uw wijzigingen niet opslaan.</span><span class="sxs-lookup"><span data-stu-id="de964-155">Replace its contents with hello following, then save your changes.</span></span>

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

### <a name="update-hello-votingwebcs-file"></a><span data-ttu-id="de964-156">Hallo VotingWeb.cs bestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="de964-156">Update hello VotingWeb.cs file</span></span>
<span data-ttu-id="de964-157">Open Hallo *VotingWeb.cs* bestand, dat Hallo ASP.NET Core WebHost binnen Hallo staatloze service met Hallo WebListener webserver maakt.</span><span class="sxs-lookup"><span data-stu-id="de964-157">Open hello *VotingWeb.cs* file, which creates hello ASP.NET Core WebHost inside hello stateless service using hello WebListener web server.</span></span>  <span data-ttu-id="de964-158">Hallo toevoegen `using System.Net.Http;` richtlijn toohello bovenaan Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="de964-158">Add hello `using System.Net.Http;` directive toohello top of hello file.</span></span>  <span data-ttu-id="de964-159">Vervang Hallo `CreateServiceInstanceListeners()` werken met de volgende Hallo en sla vervolgens uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="de964-159">Replace hello `CreateServiceInstanceListeners()` function with hello following, then save your changes.</span></span>

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

### <a name="add-hello-votescontrollercs-file"></a><span data-ttu-id="de964-160">Hallo VotesController.cs bestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="de964-160">Add hello VotesController.cs file</span></span>
<span data-ttu-id="de964-161">Een controller waarmee wordt gedefinieerd stemmende acties toevoegen.</span><span class="sxs-lookup"><span data-stu-id="de964-161">Add a controller which defines voting actions.</span></span> <span data-ttu-id="de964-162">Met de rechtermuisknop op Hallo **domeincontrollers** map, selecteer vervolgens **toevoegen -> Nieuw item -> klasse**.</span><span class="sxs-lookup"><span data-stu-id="de964-162">Right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span>  <span data-ttu-id="de964-163">Naam van bestand Hallo 'VotesController.cs' en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="de964-163">Name hello file "VotesController.cs" and click **Add**.</span></span>  <span data-ttu-id="de964-164">Bestandsinhoud Hallo vervangen door de volgende Hallo en vervolgens uw wijzigingen niet opslaan.</span><span class="sxs-lookup"><span data-stu-id="de964-164">Replace hello file contents with hello following, then save your changes.</span></span>  <span data-ttu-id="de964-165">Verderop in [updatebestand Hallo VotesController.cs](#updatevotecontroller_anchor), dit bestand wordt gewijzigd tooread en stemmende gegevens uit het back-endservice Hallo schrijven.</span><span class="sxs-lookup"><span data-stu-id="de964-165">Later, in [Update hello VotesController.cs file](#updatevotecontroller_anchor), this file will be modified tooread and write voting data from hello back-end service.</span></span>  <span data-ttu-id="de964-166">Op dit moment retourneert Hallo domeincontroller de gegevensweergave toohello vaste tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="de964-166">For now, hello controller returns static string data toohello view.</span></span>

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



### <a name="deploy-and-run-hello-application-locally"></a><span data-ttu-id="de964-167">Implementeren en het Hallo-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="de964-167">Deploy and run hello application locally</span></span>
<span data-ttu-id="de964-168">U kunt nu doorgaan en Hallo toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="de964-168">You can now go ahead and run hello application.</span></span> <span data-ttu-id="de964-169">Druk in Visual Studio op `F5` toodeploy Hallo-toepassing voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="de964-169">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span> <span data-ttu-id="de964-170">`F5`mislukt als u niet eerder Visual Studio als Open **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="de964-170">`F5` fails if you didn't previously open Visual Studio as **administrator**.</span></span>

> [!NOTE]
> <span data-ttu-id="de964-171">Hallo maakt eerst u uitvoeren en implementeren van Hallo toepassing lokaal door Visual Studio een lokaal cluster voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="de964-171">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span>  <span data-ttu-id="de964-172">Maken van het cluster kan enige tijd duren.</span><span class="sxs-lookup"><span data-stu-id="de964-172">Cluster creation may take some time.</span></span> <span data-ttu-id="de964-173">status van het Hallo-cluster maken wordt weergegeven in Visual Studio-uitvoervenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="de964-173">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="de964-174">Uw web-app moet er op dit punt wordt als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="de964-174">At this point, your web app should look like this:</span></span>

![ASP.NET Core front-](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

<span data-ttu-id="de964-176">toostop foutopsporing toepassing hello, gaat u terug tooVisual Studio en druk op **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="de964-176">toostop debugging hello application, go back tooVisual Studio and press **Shift+F5**.</span></span>

## <a name="add-a-stateful-back-end-service-tooyour-application"></a><span data-ttu-id="de964-177">Een stateful back-endservice tooyour toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="de964-177">Add a stateful back-end service tooyour application</span></span>
<span data-ttu-id="de964-178">Nu dat we een ASP.NET Web API-service die in onze toepassing wordt uitgevoerd hebben, maar eens en een stateful betrouwbare service toostore sommige gegevens in onze toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="de964-178">Now that we have an ASP.NET Web API service running in our application, let's go ahead and add a stateful reliable service toostore some data in our application.</span></span>

<span data-ttu-id="de964-179">Service Fabric kunt u tooconsistently en veilig opslaan van uw gegevens rechtstreeks in uw service met behulp van betrouwbare verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="de964-179">Service Fabric allows you tooconsistently and reliably store your data right inside your service by using reliable collections.</span></span> <span data-ttu-id="de964-180">Betrouwbare verzamelingen zijn een set van maximaal beschikbare en betrouwbare verzameling klassen die bekend tooanyone die C# verzamelingen heeft gebruikt.</span><span class="sxs-lookup"><span data-stu-id="de964-180">Reliable collections are a set of highly available and reliable collection classes that are familiar tooanyone who has used C# collections.</span></span>

<span data-ttu-id="de964-181">In deze zelfstudie maakt u een service die een itemwaarde in een betrouwbare verzameling opslaat.</span><span class="sxs-lookup"><span data-stu-id="de964-181">In this tutorial, you create a service which stores a counter value in a reliable collection.</span></span>

1. <span data-ttu-id="de964-182">Klik in Solution Explorer met de rechtermuisknop op **Services** binnen Hallo application-project en kies **toevoegen > nieuwe Service Fabric-Service**.</span><span class="sxs-lookup"><span data-stu-id="de964-182">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Een nieuwe service tooan bestaande toepassing toevoegen](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. <span data-ttu-id="de964-184">In Hallo **nieuwe Service Fabric-Service** dialoogvenster kiezen **Stateful ASP.NET Core**, en de naam Hallo service **VotingData** en druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="de964-184">In hello **New Service Fabric Service** dialog, choose **Stateful ASP.NET Core**, and name hello service **VotingData** and press **OK**.</span></span>

    ![Dialoogvenster voor nieuwe service in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    <span data-ttu-id="de964-186">Nadat uw serviceproject is gemaakt, hebt u twee services in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="de964-186">Once your service project is created, you have two services in your application.</span></span> <span data-ttu-id="de964-187">Als u toobuild uw toepassing doorgaat, kunt u meer services toevoegen in Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="de964-187">As you continue toobuild your application, you can add more services in hello same way.</span></span> <span data-ttu-id="de964-188">Elk zijn onafhankelijk samengestelde en bijgewerkte.</span><span class="sxs-lookup"><span data-stu-id="de964-188">Each can be independently versioned and upgraded.</span></span>

3. <span data-ttu-id="de964-189">de volgende pagina Hallo biedt een set van ASP.NET Core projectsjablonen.</span><span class="sxs-lookup"><span data-stu-id="de964-189">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="de964-190">Voor deze zelfstudie kiest **Web API**.</span><span class="sxs-lookup"><span data-stu-id="de964-190">For this tutorial, choose **Web API**.</span></span>

    ![ASP.NET-project kiezen](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    <span data-ttu-id="de964-192">Visual Studio maakt een serviceproject en geeft deze weer in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="de964-192">Visual Studio creates a service project and displays them in Solution Explorer.</span></span>

    ![Solution Explorer](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a><span data-ttu-id="de964-194">Hallo VoteDataController.cs bestand toevoegen</span><span class="sxs-lookup"><span data-stu-id="de964-194">Add hello VoteDataController.cs file</span></span>

<span data-ttu-id="de964-195">In Hallo **VotingData** project met de rechtermuisknop op Hallo **domeincontrollers** map, selecteer vervolgens **toevoegen -> Nieuw item -> klasse**.</span><span class="sxs-lookup"><span data-stu-id="de964-195">In hello **VotingData** project right-click on hello **Controllers** folder, then select **Add->New item->Class**.</span></span> <span data-ttu-id="de964-196">Naam van bestand Hallo 'VoteDataController.cs' en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="de964-196">Name hello file "VoteDataController.cs" and click **Add**.</span></span> <span data-ttu-id="de964-197">Bestandsinhoud Hallo vervangen door de volgende Hallo en vervolgens uw wijzigingen niet opslaan.</span><span class="sxs-lookup"><span data-stu-id="de964-197">Replace hello file contents with hello following, then save your changes.</span></span>

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


## <a name="connect-hello-services"></a><span data-ttu-id="de964-198">Verbinding maken met de Hallo-services</span><span class="sxs-lookup"><span data-stu-id="de964-198">Connect hello services</span></span>
<span data-ttu-id="de964-199">In deze stap, we Hallo twee services verbinding en zorg Hallo front-end Web application get en set gegevens uit het back-endservice Hallo stemmen.</span><span class="sxs-lookup"><span data-stu-id="de964-199">In this next step, we will connect hello two services and make hello front-end Web application get and set voting information from hello back-end service.</span></span>

<span data-ttu-id="de964-200">Service Fabric biedt volledige flexibiliteit in hoe u met reliable services communiceren.</span><span class="sxs-lookup"><span data-stu-id="de964-200">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="de964-201">Binnen één toepassing hebt u mogelijk services die toegankelijk via TCP zijn.</span><span class="sxs-lookup"><span data-stu-id="de964-201">Within a single application, you might have services that are accessible via TCP.</span></span> <span data-ttu-id="de964-202">Andere services die mogelijk toegankelijk via een HTTP REST-API en nog andere services kunnen toegang worden verkregen via websockets.</span><span class="sxs-lookup"><span data-stu-id="de964-202">Other services that might be accessible via an HTTP REST API and still other services could be accessible via web sockets.</span></span> <span data-ttu-id="de964-203">Zie voor achtergrondinformatie over Hallo opties die beschikbaar zijn en Hallo-en nadelen betrokken [services communiceert](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="de964-203">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span>

<span data-ttu-id="de964-204">In deze zelfstudie gebruiken we [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="de964-204">In this tutorial, we are using [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a><span data-ttu-id="de964-205">Hallo VotesController.cs bestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="de964-205">Update hello VotesController.cs file</span></span>
<span data-ttu-id="de964-206">In Hallo **VotingWeb** project, open Hallo *Controllers/VotesController.cs* bestand.</span><span class="sxs-lookup"><span data-stu-id="de964-206">In hello **VotingWeb** project, open hello *Controllers/VotesController.cs* file.</span></span>  <span data-ttu-id="de964-207">Vervang Hallo `VotesController` definitie inhoud met de volgende Hallo klasse en sla vervolgens uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="de964-207">Replace hello `VotesController` class definition contents with hello following, then save your changes.</span></span>

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

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="de964-208">Hallo stemmen voorbeeldtoepassing doorlopen</span><span class="sxs-lookup"><span data-stu-id="de964-208">Walk through hello voting sample application</span></span>
<span data-ttu-id="de964-209">Hallo stemmen toepassing bestaat uit twee services:</span><span class="sxs-lookup"><span data-stu-id="de964-209">hello voting application consists of two services:</span></span>
- <span data-ttu-id="de964-210">Web-front-service (VotingWeb): een ASP.NET Core web-front-endservice die webpagina Hallo fungeert en zichtbaar gemaakt web-API's toocommunicate met Hallo back-endservice.</span><span class="sxs-lookup"><span data-stu-id="de964-210">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="de964-211">Back-end-service (VotingData)-Core van een ASP.NET-webservice, die zichtbaar gemaakt die een API toostore Hallo stem in een betrouwbare woordenlijst resulteert op schijf persistent.</span><span class="sxs-lookup"><span data-stu-id="de964-211">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Diagram van de toepassing](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

<span data-ttu-id="de964-213">Wanneer u stemmen in Hallo toepassing hello volgende gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="de964-213">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="de964-214">Een JavaScript verzendt Hallo stem aanvraag toohello web API in Hallo web-front-service als een HTTP PUT-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="de964-214">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="de964-215">Hallo-web-front-service gebruikt een toolocate proxy en doorsturen van een HTTP PUT-aanvraag toohello back-endservice.</span><span class="sxs-lookup"><span data-stu-id="de964-215">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="de964-216">Hallo back-endservice Hallo inkomende aanvraag duurt en winkels Hallo bijgewerkt resulteren in een betrouwbare woordenlijst die gerepliceerde toomultiple knooppunten binnen Hallo cluster opgehaald en opgeslagen op schijf.</span><span class="sxs-lookup"><span data-stu-id="de964-216">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="de964-217">Alle Hallo toepassingsgegevens wordt opgeslagen in Hallo-cluster, zodat er geen database nodig is.</span><span class="sxs-lookup"><span data-stu-id="de964-217">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="de964-218">Fouten opsporen in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="de964-218">Debug in Visual Studio</span></span>
<span data-ttu-id="de964-219">Als u fouten opspoort toepassing in Visual Studio, gebruikt u een lokaal cluster van de Service Fabric-ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="de964-219">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="de964-220">U hebt uw foutopsporing ervaring tooyour scenario Hallo optie tooadjust.</span><span class="sxs-lookup"><span data-stu-id="de964-220">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="de964-221">In deze toepassing opgeslagen gegevens in onze back-end-service met behulp van een betrouwbare woordenlijst.</span><span class="sxs-lookup"><span data-stu-id="de964-221">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="de964-222">Visual Studio Hiermee verwijdert u de toepassing hello per standaard wanneer u Hallo foutopsporingsprogramma stopt.</span><span class="sxs-lookup"><span data-stu-id="de964-222">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="de964-223">Verwijderen van de toepassing hello zorgt ervoor dat de gegevens Hallo in Hallo back-end service tooalso worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="de964-223">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="de964-224">toopersist hello gegevens tussen foutopsporingssessies, kunt u Hallo **toepassing foutopsporingsmodus** als eigenschap op Hallo **Voting** -project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de964-224">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="de964-225">toolook op wat er gebeurt in Hallo code voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="de964-225">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="de964-226">Open Hallo **VotesController.cs** bestands- en stel een onderbrekingspunt in Hallo web-API's **plaatsen** methode (regel 47) - u kunt zoeken naar Hallo-bestand in Hallo Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de964-226">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="de964-227">Open Hallo **VoteDataController.cs** bestands- en stel een onderbrekingspunt in deze web-API **plaatsen** methode (line 50).</span><span class="sxs-lookup"><span data-stu-id="de964-227">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="de964-228">Ga terug toohello browser en klik op een optie of toevoegen van een nieuwe stemmende optie.</span><span class="sxs-lookup"><span data-stu-id="de964-228">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="de964-229">U onderbrekingspunt Hallo eerste in Hallo web front-end van api-controller.</span><span class="sxs-lookup"><span data-stu-id="de964-229">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    
    1. <span data-ttu-id="de964-230">Dit is waar Hallo JavaScript in browser Hallo verzendt u een aanvraag toohello web API-controller in Hallo front-end-service.</span><span class="sxs-lookup"><span data-stu-id="de964-230">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Stem front-end-Service toevoegen](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. <span data-ttu-id="de964-232">Eerst we Hallo URL toohello ReverseProxy opstellen voor onze back-endservice **(1)**.</span><span class="sxs-lookup"><span data-stu-id="de964-232">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    3. <span data-ttu-id="de964-233">Vervolgens we Hallo HTTP PUT-aanvraag toohello ReverseProxy sturen **(2)**.</span><span class="sxs-lookup"><span data-stu-id="de964-233">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    4. <span data-ttu-id="de964-234">Ten slotte hello wordt teruggeplaatst antwoord Hallo van Hallo back-endservice toohello client **(3)**.</span><span class="sxs-lookup"><span data-stu-id="de964-234">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="de964-235">Druk op **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="de964-235">Press **F5** toocontinue</span></span>
    1. <span data-ttu-id="de964-236">U bent nu op Hallo break punt in Hallo back-endservice.</span><span class="sxs-lookup"><span data-stu-id="de964-236">You are now at hello break point in hello back-end service.</span></span>
    
    ![Stem Back-End-Service toevoegen](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. <span data-ttu-id="de964-238">In de eerste regel in de methode Hallo Hallo **(1)** gebruiken we Hallo `StateManager` tooget of toevoegen van een betrouwbare woordenlijst aangeroepen `counts`.</span><span class="sxs-lookup"><span data-stu-id="de964-238">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    3. <span data-ttu-id="de964-239">Alle interacties met waarden in een betrouwbare woordenlijst vereisen een transactie, deze met de instructie **(2)** die transactie maakt.</span><span class="sxs-lookup"><span data-stu-id="de964-239">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    4. <span data-ttu-id="de964-240">In de transactie hello, werk we vervolgens Hallo-waarde van relevante Hallo-sleutel voor uw stem optie Hallo en doorvoeracties Hallo bewerking **(3)**.</span><span class="sxs-lookup"><span data-stu-id="de964-240">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="de964-241">Zodra het Hallo doorvoeren retourneert methode, Hallo gegevens wordt bijgewerkt in de woordenlijst Hallo en tooother knooppunten in cluster Hallo gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="de964-241">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="de964-242">Hallo gegevens worden nu veilig opgeslagen in de cluster Hallo en Hallo back-endservice failover tooother knooppunten, nog steeds Hallo gegevens beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="de964-242">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="de964-243">Druk op **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="de964-243">Press **F5** toocontinue</span></span>

<span data-ttu-id="de964-244">toostop hello foutopsporingssessie, drukt u op **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="de964-244">toostop hello debugging session, press **Shift+F5**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="de964-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de964-245">Next steps</span></span>
<span data-ttu-id="de964-246">In dit deel van de zelfstudie hello, hebt u geleerd hoe:</span><span class="sxs-lookup"><span data-stu-id="de964-246">In this part of hello tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="de964-247">Een ASP.NET Core Web API-service als betrouwbare stateful service maken</span><span class="sxs-lookup"><span data-stu-id="de964-247">Create an ASP.NET Core Web API service as a stateful reliable service</span></span>
> * <span data-ttu-id="de964-248">Een ASP.NET-webtoepassing Core-service als een stateless webservice maken</span><span class="sxs-lookup"><span data-stu-id="de964-248">Create an ASP.NET Core Web Application service as a stateless web service</span></span>
> * <span data-ttu-id="de964-249">Hallo omgekeerde proxy toocommunicate Hallo stateful service gebruiken</span><span class="sxs-lookup"><span data-stu-id="de964-249">Use hello reverse proxy toocommunicate with hello stateful service</span></span>

<span data-ttu-id="de964-250">Geavanceerde toohello volgende zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="de964-250">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="de964-251">Hallo toepassing tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="de964-251">Deploy hello application tooAzure</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)

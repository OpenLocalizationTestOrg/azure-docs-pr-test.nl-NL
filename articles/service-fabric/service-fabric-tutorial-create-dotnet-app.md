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
# <a name="create-and-deploy-an-application-with-an-aspnet-core-web-api-front-end-service-and-a-stateful-back-end-service"></a>Maken en implementeren van een toepassing met een front-ASP.NET Core Web API-service en een stateful back-endservice
Deze zelfstudie maakt deel uit een reeks.  U leert hoe toocreate een Azure Service Fabric-toepassing met een Web-API van ASP.NET Core front end en een stateful back-endservice toostore uw gegevens. Wanneer u klaar bent, hebt u een stemtoepassing met een ASP.NET Core web-front-die stemmende resultaten worden opgeslagen in een stateful back-end-service in Hallo-cluster. Als u niet wilt dat toomanually Hallo stemmen toepassing maken, kunt u [Hallo broncode downloaden](https://github.com/Azure-Samples/service-fabric-dotnet-quickstart/) voor Hallo voltooid toepassing en gaat u verder te[doorlopen Hallo stemmen voorbeeldtoepassing](#walkthrough_anchor).

![Diagram van de toepassing](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Deel een reeks hello, leert u hoe:

> [!div class="checklist"]
> * Een ASP.NET Core Web API-service als betrouwbare stateful service maken
> * Een ASP.NET-webtoepassing Core-service als een stateless webservice maken
> * Hallo omgekeerde proxy toocommunicate Hallo stateful service gebruiken

In deze zelfstudie reeks leert u hoe:
> [!div class="checklist"]
> * Een .NET-Service Fabric-toepassing bouwen
> * [Hallo toepassing tooa RAS-cluster implementeren](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * [CI/CD met behulp van Visual Studio Team Services configureren](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint:
- Als u geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- [Installeer Visual Studio 2017](https://www.visualstudio.com/) en installeer Hallo **ontwikkelen van Azure** en **ASP.NET en web ontwikkeling** werkbelastingen.
- [Hallo Service Fabric SDK installeren](service-fabric-get-started.md)

## <a name="create-an-aspnet-web-api-service-as-a-reliable-service"></a>Een ASP.NET Web API-service als een betrouwbare service maken
Maak eerst Hallo web front-Hallo stemmen toepassing via ASP.NET Core. ASP.NET Core is een lichtgewicht, platformoverschrijdende ontwikkeling webframework toocreate moderne webgebruikersinterface gebruiken en web-API's. een volledig begrip van hoe ASP.NET Core met Service Fabric integreert tooget, wordt aangeraden lezen via Hallo [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) artikel. Op dit moment kunt u deze zelfstudie tooget snel aan de slag. toolearn meer informatie over ASP.NET Core, Zie Hallo [ASP.NET Core documentatie](https://docs.microsoft.com/aspnet/core/).

> [!NOTE]
> Deze zelfstudie is gebaseerd op Hallo [ASP.NET Core tools voor Visual Studio 2017](https://docs.microsoft.com/aspnet/core/tutorials/first-mvc-app/start-mvc). Hallo .NET Core tools voor Visual Studio 2015 worden niet langer bijgewerkt.

1. Start Visual Studio als **beheerder**.

2. Maken van een project met **bestand**->**nieuw**->**Project**

3. In Hallo **nieuw Project** dialoogvenster kiezen **Cloud > Service Fabric-toepassing**.

4. Naam van de toepassing hello **Voting** en druk op **OK**.

   ![Dialoogvenster voor nieuw project in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog.png)

5. Op Hallo **nieuwe Service Fabric-Service** pagina **staatloze ASP.NET Core**, en de naam van uw service **VotingWeb**.
   
   ![ASP.NET-webservice te kiezen in het dialoogvenster voor nieuwe service Hallo](./media/service-fabric-tutorial-create-dotnet-app/new-project-dialog-2.png) 

6. de volgende pagina Hallo biedt een set van ASP.NET Core projectsjablonen. Voor deze zelfstudie kiest **webtoepassing**. 
   
   ![ASP.NET-project kiezen](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog.png)

   Visual Studio maakt een toepassing en een serviceproject en geeft deze weer in Solution Explorer.

   ![Solution Explorer na het maken van een toepassing met ASP.NET core Web API-service]( ./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-angularjs-toohello-votingweb-service"></a>AngularJS toohello VotingWeb service toevoegen
Voeg [AngularJS](http://angularjs.org/) tooyour service met behulp van de ingebouwde Hallo [Bower ondersteuning](/aspnet/core/client-side/bower). Open *bower.json* en vermeldingen voor hoeken en hoekvormige bootstrap toevoegen en vervolgens uw wijzigingen niet opslaan.

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
Bij het opslaan van Hallo *bower.json* bestand Angular is geïnstalleerd in uw project *wwwroot/lib* map. Bovendien wordt vermeld in Hallo *afhankelijkheden/Bower* map.

### <a name="update-hello-sitejs-file"></a>Hallo site.js bestand bijwerken
Open Hallo *wwwroot/js/site.js* bestand.  De inhoud ervan vervangen door Hallo JavaScript gebruikt door Hallo Home weergaven:

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

### <a name="update-hello-indexcshtml-file"></a>Hallo Index.cshtml bestand bijwerken
Open Hallo *Views/Home/Index.cshtml* bestand, Hallo specifieke toohello Home weergavebesturing.  Vervang de inhoud door de volgende Hallo en vervolgens uw wijzigingen niet opslaan.

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

### <a name="update-hello-layoutcshtml-file"></a>Hallo _Layout.cshtml bestand bijwerken
Open Hallo *Views/Shared/_Layout.cshtml* bestand, Hallo standaardindeling voor Hallo ASP.NET-app.  Vervang de inhoud door de volgende Hallo en vervolgens uw wijzigingen niet opslaan.

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

### <a name="update-hello-votingwebcs-file"></a>Hallo VotingWeb.cs bestand bijwerken
Open Hallo *VotingWeb.cs* bestand, dat Hallo ASP.NET Core WebHost binnen Hallo staatloze service met Hallo WebListener webserver maakt.  Hallo toevoegen `using System.Net.Http;` richtlijn toohello bovenaan Hallo-bestand.  Vervang Hallo `CreateServiceInstanceListeners()` werken met de volgende Hallo en sla vervolgens uw wijzigingen.

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

### <a name="add-hello-votescontrollercs-file"></a>Hallo VotesController.cs bestand toevoegen
Een controller waarmee wordt gedefinieerd stemmende acties toevoegen. Met de rechtermuisknop op Hallo **domeincontrollers** map, selecteer vervolgens **toevoegen -> Nieuw item -> klasse**.  Naam van bestand Hallo 'VotesController.cs' en klik op **toevoegen**.  Bestandsinhoud Hallo vervangen door de volgende Hallo en vervolgens uw wijzigingen niet opslaan.  Verderop in [updatebestand Hallo VotesController.cs](#updatevotecontroller_anchor), dit bestand wordt gewijzigd tooread en stemmende gegevens uit het back-endservice Hallo schrijven.  Op dit moment retourneert Hallo domeincontroller de gegevensweergave toohello vaste tekenreeks.

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



### <a name="deploy-and-run-hello-application-locally"></a>Implementeren en het Hallo-toepassing lokaal uitvoeren
U kunt nu doorgaan en Hallo toepassing uitvoeren. Druk in Visual Studio op `F5` toodeploy Hallo-toepassing voor foutopsporing. `F5`mislukt als u niet eerder Visual Studio als Open **beheerder**.

> [!NOTE]
> Hallo maakt eerst u uitvoeren en implementeren van Hallo toepassing lokaal door Visual Studio een lokaal cluster voor foutopsporing.  Maken van het cluster kan enige tijd duren. status van het Hallo-cluster maken wordt weergegeven in Visual Studio-uitvoervenster Hallo.

Uw web-app moet er op dit punt wordt als volgt uitzien:

![ASP.NET Core front-](./media/service-fabric-tutorial-create-dotnet-app/debug-front-end.png)

toostop foutopsporing toepassing hello, gaat u terug tooVisual Studio en druk op **Shift + F5**.

## <a name="add-a-stateful-back-end-service-tooyour-application"></a>Een stateful back-endservice tooyour toepassing toevoegen
Nu dat we een ASP.NET Web API-service die in onze toepassing wordt uitgevoerd hebben, maar eens en een stateful betrouwbare service toostore sommige gegevens in onze toepassing toevoegen.

Service Fabric kunt u tooconsistently en veilig opslaan van uw gegevens rechtstreeks in uw service met behulp van betrouwbare verzamelingen. Betrouwbare verzamelingen zijn een set van maximaal beschikbare en betrouwbare verzameling klassen die bekend tooanyone die C# verzamelingen heeft gebruikt.

In deze zelfstudie maakt u een service die een itemwaarde in een betrouwbare verzameling opslaat.

1. Klik in Solution Explorer met de rechtermuisknop op **Services** binnen Hallo application-project en kies **toevoegen > nieuwe Service Fabric-Service**.
   
    ![Een nieuwe service tooan bestaande toepassing toevoegen](./media/service-fabric-tutorial-create-dotnet-app/vs-add-new-service.png)

2. In Hallo **nieuwe Service Fabric-Service** dialoogvenster kiezen **Stateful ASP.NET Core**, en de naam Hallo service **VotingData** en druk op **OK**.

    ![Dialoogvenster voor nieuwe service in Visual Studio](./media/service-fabric-tutorial-create-dotnet-app/add-stateful-service.png)

    Nadat uw serviceproject is gemaakt, hebt u twee services in uw toepassing. Als u toobuild uw toepassing doorgaat, kunt u meer services toevoegen in Hallo dezelfde manier. Elk zijn onafhankelijk samengestelde en bijgewerkte.

3. de volgende pagina Hallo biedt een set van ASP.NET Core projectsjablonen. Voor deze zelfstudie kiest **Web API**.

    ![ASP.NET-project kiezen](./media/service-fabric-tutorial-create-dotnet-app/vs-new-aspnet-project-dialog2.png)

    Visual Studio maakt een serviceproject en geeft deze weer in Solution Explorer.

    ![Solution Explorer](./media/service-fabric-tutorial-create-dotnet-app/solution-explorer-aspnetcore-service.png)

### <a name="add-hello-votedatacontrollercs-file"></a>Hallo VoteDataController.cs bestand toevoegen

In Hallo **VotingData** project met de rechtermuisknop op Hallo **domeincontrollers** map, selecteer vervolgens **toevoegen -> Nieuw item -> klasse**. Naam van bestand Hallo 'VoteDataController.cs' en klik op **toevoegen**. Bestandsinhoud Hallo vervangen door de volgende Hallo en vervolgens uw wijzigingen niet opslaan.

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


## <a name="connect-hello-services"></a>Verbinding maken met de Hallo-services
In deze stap, we Hallo twee services verbinding en zorg Hallo front-end Web application get en set gegevens uit het back-endservice Hallo stemmen.

Service Fabric biedt volledige flexibiliteit in hoe u met reliable services communiceren. Binnen één toepassing hebt u mogelijk services die toegankelijk via TCP zijn. Andere services die mogelijk toegankelijk via een HTTP REST-API en nog andere services kunnen toegang worden verkregen via websockets. Zie voor achtergrondinformatie over Hallo opties die beschikbaar zijn en Hallo-en nadelen betrokken [services communiceert](service-fabric-connect-and-communicate-with-services.md).

In deze zelfstudie gebruiken we [ASP.NET Core Web API](service-fabric-reliable-services-communication-aspnetcore.md).

<a id="updatevotecontroller" name="updatevotecontroller_anchor"></a>

### <a name="update-hello-votescontrollercs-file"></a>Hallo VotesController.cs bestand bijwerken
In Hallo **VotingWeb** project, open Hallo *Controllers/VotesController.cs* bestand.  Vervang Hallo `VotesController` definitie inhoud met de volgende Hallo klasse en sla vervolgens uw wijzigingen.

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

## <a name="walk-through-hello-voting-sample-application"></a>Hallo stemmen voorbeeldtoepassing doorlopen
Hallo stemmen toepassing bestaat uit twee services:
- Web-front-service (VotingWeb): een ASP.NET Core web-front-endservice die webpagina Hallo fungeert en zichtbaar gemaakt web-API's toocommunicate met Hallo back-endservice.
- Back-end-service (VotingData)-Core van een ASP.NET-webservice, die zichtbaar gemaakt die een API toostore Hallo stem in een betrouwbare woordenlijst resulteert op schijf persistent.

![Diagram van de toepassing](./media/service-fabric-tutorial-create-dotnet-app/application-diagram.png)

Wanneer u stemmen in Hallo toepassing hello volgende gebeurtenissen:
1. Een JavaScript verzendt Hallo stem aanvraag toohello web API in Hallo web-front-service als een HTTP PUT-aanvraag.

2. Hallo-web-front-service gebruikt een toolocate proxy en doorsturen van een HTTP PUT-aanvraag toohello back-endservice.

3. Hallo back-endservice Hallo inkomende aanvraag duurt en winkels Hallo bijgewerkt resulteren in een betrouwbare woordenlijst die gerepliceerde toomultiple knooppunten binnen Hallo cluster opgehaald en opgeslagen op schijf. Alle Hallo toepassingsgegevens wordt opgeslagen in Hallo-cluster, zodat er geen database nodig is.

## <a name="debug-in-visual-studio"></a>Fouten opsporen in Visual Studio
Als u fouten opspoort toepassing in Visual Studio, gebruikt u een lokaal cluster van de Service Fabric-ontwikkeling. U hebt uw foutopsporing ervaring tooyour scenario Hallo optie tooadjust. In deze toepassing opgeslagen gegevens in onze back-end-service met behulp van een betrouwbare woordenlijst. Visual Studio Hiermee verwijdert u de toepassing hello per standaard wanneer u Hallo foutopsporingsprogramma stopt. Verwijderen van de toepassing hello zorgt ervoor dat de gegevens Hallo in Hallo back-end service tooalso worden verwijderd. toopersist hello gegevens tussen foutopsporingssessies, kunt u Hallo **toepassing foutopsporingsmodus** als eigenschap op Hallo **Voting** -project in Visual Studio.

toolook op wat er gebeurt in Hallo code voltooid Hallo stappen te volgen:
1. Open Hallo **VotesController.cs** bestands- en stel een onderbrekingspunt in Hallo web-API's **plaatsen** methode (regel 47) - u kunt zoeken naar Hallo-bestand in Hallo Solution Explorer in Visual Studio.

2. Open Hallo **VoteDataController.cs** bestands- en stel een onderbrekingspunt in deze web-API **plaatsen** methode (line 50).

3. Ga terug toohello browser en klik op een optie of toevoegen van een nieuwe stemmende optie. U onderbrekingspunt Hallo eerste in Hallo web front-end van api-controller.
    
    1. Dit is waar Hallo JavaScript in browser Hallo verzendt u een aanvraag toohello web API-controller in Hallo front-end-service.
    
    ![Stem front-end-Service toevoegen](./media/service-fabric-tutorial-create-dotnet-app/addvote-frontend.png)

    2. Eerst we Hallo URL toohello ReverseProxy opstellen voor onze back-endservice **(1)**.
    3. Vervolgens we Hallo HTTP PUT-aanvraag toohello ReverseProxy sturen **(2)**.
    4. Ten slotte hello wordt teruggeplaatst antwoord Hallo van Hallo back-endservice toohello client **(3)**.

4. Druk op **F5** toocontinue
    1. U bent nu op Hallo break punt in Hallo back-endservice.
    
    ![Stem Back-End-Service toevoegen](./media/service-fabric-tutorial-create-dotnet-app/addvote-backend.png)

    2. In de eerste regel in de methode Hallo Hallo **(1)** gebruiken we Hallo `StateManager` tooget of toevoegen van een betrouwbare woordenlijst aangeroepen `counts`.
    3. Alle interacties met waarden in een betrouwbare woordenlijst vereisen een transactie, deze met de instructie **(2)** die transactie maakt.
    4. In de transactie hello, werk we vervolgens Hallo-waarde van relevante Hallo-sleutel voor uw stem optie Hallo en doorvoeracties Hallo bewerking **(3)**. Zodra het Hallo doorvoeren retourneert methode, Hallo gegevens wordt bijgewerkt in de woordenlijst Hallo en tooother knooppunten in cluster Hallo gerepliceerd. Hallo gegevens worden nu veilig opgeslagen in de cluster Hallo en Hallo back-endservice failover tooother knooppunten, nog steeds Hallo gegevens beschikbaar.
5. Druk op **F5** toocontinue

toostop hello foutopsporingssessie, drukt u op **Shift + F5**.


## <a name="next-steps"></a>Volgende stappen
In dit deel van de zelfstudie hello, hebt u geleerd hoe:

> [!div class="checklist"]
> * Een ASP.NET Core Web API-service als betrouwbare stateful service maken
> * Een ASP.NET-webtoepassing Core-service als een stateless webservice maken
> * Hallo omgekeerde proxy toocommunicate Hallo stateful service gebruiken

Geavanceerde toohello volgende zelfstudie:
> [!div class="nextstepaction"]
> [Hallo toepassing tooAzure implementeren](service-fabric-tutorial-deploy-app-to-party-cluster.md)

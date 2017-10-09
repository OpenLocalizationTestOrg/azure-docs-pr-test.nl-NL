---
title: een webfront-end voor uw Azure Service Fabric-app met behulp van ASP.NET Core aaaCreate | Microsoft Docs
description: Uw web-Service Fabric-toepassing toohello weergeven met behulp van een ASP.NET Core project en service-interne communicatie via de Service voor externe toegang.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: vturecek
ms.openlocfilehash: 0c4454d6cac4c2e343bd6e93e56d3d2f0ebfc4ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-web-service-front-end-for-your-application-using-aspnet-core"></a><span data-ttu-id="dfef2-103">Een service webfront-end voor uw toepassing met behulp van ASP.NET Core bouwen</span><span class="sxs-lookup"><span data-stu-id="dfef2-103">Build a web service front end for your application using ASP.NET Core</span></span>
<span data-ttu-id="dfef2-104">Azure Service Fabric-services bieden standaard geen een openbare interface toohello web.</span><span class="sxs-lookup"><span data-stu-id="dfef2-104">By default, Azure Service Fabric services do not provide a public interface toohello web.</span></span> <span data-ttu-id="dfef2-105">tooexpose van uw toepassing functionaliteit tooHTTP clients, hebt u toocreate een web project tooact als een toegangspunt en vervolgens communiceren van er tooyour afzonderlijke services.</span><span class="sxs-lookup"><span data-stu-id="dfef2-105">tooexpose your application's functionality tooHTTP clients, you have toocreate a web project tooact as an entry point and then communicate from there tooyour individual services.</span></span>

<span data-ttu-id="dfef2-106">In deze zelfstudie gaan we waar we werd afgebroken in Hallo [maken van uw eerste toepassing in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) zelfstudie en een webservice ASP.NET Core voren Hallo teller stateful service toevoegen.</span><span class="sxs-lookup"><span data-stu-id="dfef2-106">In this tutorial, we pick up where we left off in hello [Creating your first application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md) tutorial and add an ASP.NET Core web service in front of hello stateful counter service.</span></span> <span data-ttu-id="dfef2-107">Als u dit nog niet hebt gedaan, moet u teruggaan en deze zelfstudie eerst doorlopen.</span><span class="sxs-lookup"><span data-stu-id="dfef2-107">If you have not already done so, you should go back and step through that tutorial first.</span></span>

## <a name="set-up-your-environment-for-aspnet-core"></a><span data-ttu-id="dfef2-108">Instellen van uw omgeving voor ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="dfef2-108">Set up your environment for ASP.NET Core</span></span>

<span data-ttu-id="dfef2-109">Moet u Visual Studio 2017 toofollow samen met deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="dfef2-109">You need Visual Studio 2017 toofollow along with this tutorial.</span></span> <span data-ttu-id="dfef2-110">Elke editie wordt gedaan.</span><span class="sxs-lookup"><span data-stu-id="dfef2-110">Any edition will do.</span></span> 

 - [<span data-ttu-id="dfef2-111">Visual Studio 2017 installeren</span><span class="sxs-lookup"><span data-stu-id="dfef2-111">Install Visual Studio 2017</span></span>](https://www.visualstudio.com/)

<span data-ttu-id="dfef2-112">toodevelop ASP.NET Core Service Fabric-toepassingen, moet u Hallo volgende van werkbelastingen geïnstalleerd hebben:</span><span class="sxs-lookup"><span data-stu-id="dfef2-112">toodevelop ASP.NET Core Service Fabric applications, you should have hello following workloads installed:</span></span>
 - <span data-ttu-id="dfef2-113">**Ontwikkelen van Azure** (onder *Web- en Cloud*)</span><span class="sxs-lookup"><span data-stu-id="dfef2-113">**Azure development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="dfef2-114">**ASP.NET- en web ontwikkeling** (onder *Web- en Cloud*)</span><span class="sxs-lookup"><span data-stu-id="dfef2-114">**ASP.NET and web development** (under *Web & Cloud*)</span></span>
 - <span data-ttu-id="dfef2-115">**.NET core platformoverschrijdende ontwikkeling** (onder *andere Toolsets*)</span><span class="sxs-lookup"><span data-stu-id="dfef2-115">**.NET Core cross-platform development** (under *Other Toolsets*)</span></span>

>[!Note] 
><span data-ttu-id="dfef2-116">Hallo .NET Core tools voor Visual Studio 2015 zijn niet langer wordt bijgewerkt, maar als u nog steeds Visual Studio 2015 gebruikt, u toohave moet [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="dfef2-116">hello .NET Core tools for Visual Studio 2015 are no longer being updated, however if you are still using Visual Studio 2015, you need toohave [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="add-an-aspnet-core-service-tooyour-application"></a><span data-ttu-id="dfef2-117">Een ASP.NET Core service tooyour toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="dfef2-117">Add an ASP.NET Core service tooyour application</span></span>
<span data-ttu-id="dfef2-118">ASP.NET Core is een lichtgewicht, platformoverschrijdende ontwikkeling webframework toocreate moderne webgebruikersinterface gebruiken en web-API's.</span><span class="sxs-lookup"><span data-stu-id="dfef2-118">ASP.NET Core is a lightweight, cross-platform web development framework that you can use toocreate modern web UI and web APIs.</span></span> 

<span data-ttu-id="dfef2-119">We gaan een ASP.NET Web API-project tooour bestaande toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="dfef2-119">Let's add an ASP.NET Web API project tooour existing application.</span></span>

1. <span data-ttu-id="dfef2-120">Klik in Solution Explorer met de rechtermuisknop op **Services** binnen Hallo application-project en kies **toevoegen > nieuwe Service Fabric-Service**.</span><span class="sxs-lookup"><span data-stu-id="dfef2-120">In Solution Explorer, right-click **Services** within hello application project and choose **Add > New Service Fabric Service**.</span></span>
   
    ![Een nieuwe service tooan bestaande toepassing toevoegen][vs-add-new-service]
2. <span data-ttu-id="dfef2-122">Op Hallo **maken van een Service** pagina **ASP.NET Core** en een naam geven.</span><span class="sxs-lookup"><span data-stu-id="dfef2-122">On hello **Create a Service** page, choose **ASP.NET Core** and give it a name.</span></span>
   
    ![ASP.NET-webservice te kiezen in het dialoogvenster voor nieuwe service Hallo][vs-new-service-dialog]

3. <span data-ttu-id="dfef2-124">de volgende pagina Hallo biedt een set van ASP.NET Core projectsjablonen.</span><span class="sxs-lookup"><span data-stu-id="dfef2-124">hello next page provides a set of ASP.NET Core project templates.</span></span> <span data-ttu-id="dfef2-125">Opmerking dat deze identiek zijn Hallo keuzes die u zou zien als u een project ASP.NET Core buiten een Service Fabric-toepassing hebt gemaakt met een kleine hoeveelheid aanvullende code tooregister Hallo service met de Hallo Service Fabric-runtime.</span><span class="sxs-lookup"><span data-stu-id="dfef2-125">Note that these are hello same choices that you would see if you created an ASP.NET Core project outside of a Service Fabric application, with a small amount of additional code tooregister hello service with hello Service Fabric runtime.</span></span> <span data-ttu-id="dfef2-126">Voor deze zelfstudie kiest **Web API**.</span><span class="sxs-lookup"><span data-stu-id="dfef2-126">For this tutorial, choose **Web API**.</span></span> <span data-ttu-id="dfef2-127">U kunt echter toepassen Hallo dezelfde concepten toobuilding een volledige webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="dfef2-127">However, you can apply hello same concepts toobuilding a full web application.</span></span>
   
    ![ASP.NET-projecttype kiezen][vs-new-aspnet-project-dialog]
   
    <span data-ttu-id="dfef2-129">Zodra uw Web API-project is gemaakt, hebt u twee services in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="dfef2-129">Once your Web API project is created, you should have two services in your application.</span></span> <span data-ttu-id="dfef2-130">Als u toobuild uw toepassing doorgaat, kunt u meer services toevoegen in exact Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="dfef2-130">As you continue toobuild your application, you can add more services in exactly hello same way.</span></span> <span data-ttu-id="dfef2-131">Elk zijn onafhankelijk samengestelde en bijgewerkte.</span><span class="sxs-lookup"><span data-stu-id="dfef2-131">Each can be independently versioned and upgraded.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="dfef2-132">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="dfef2-132">Run hello application</span></span>
<span data-ttu-id="dfef2-133">tooget een beeld krijgt van wat we hebt gedaan, gaan we implementeren de nieuwe toepassing hello en los het bekijkt hello standaardgedrag dat ASP.NET Core Web API-sjabloon Hallo biedt.</span><span class="sxs-lookup"><span data-stu-id="dfef2-133">tooget a sense of what we've done, let's deploy hello new application and take a look at hello default behavior that hello ASP.NET Core Web API template provides.</span></span>

1. <span data-ttu-id="dfef2-134">Druk op F5 in Visual Studio toodebug Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="dfef2-134">Press F5 in Visual Studio toodebug hello app.</span></span>
2. <span data-ttu-id="dfef2-135">Wanneer de implementatie is voltooid, Start Visual Studio een browser toohello basis Hallo ASP.NET Web API-service.</span><span class="sxs-lookup"><span data-stu-id="dfef2-135">When deployment is complete, Visual Studio launches a browser toohello root of hello ASP.NET Web API service.</span></span> <span data-ttu-id="dfef2-136">Hallo ASP.NET Core Web API-sjabloon biedt niet standaardgedrag voor Hallo toegangspunt, zodat u een 404-fout in de browser Hallo ziet.</span><span class="sxs-lookup"><span data-stu-id="dfef2-136">hello ASP.NET Core Web API template doesn't provide default behavior for hello root, so you should see a 404 error in hello browser.</span></span>
3. <span data-ttu-id="dfef2-137">Voeg `/api/values` toohello locatie in Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="dfef2-137">Add `/api/values` toohello location in hello browser.</span></span> <span data-ttu-id="dfef2-138">Hiermee wordt Hallo `Get` methode op Hallo ValuesController in Hallo Web API-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="dfef2-138">This invokes hello `Get` method on hello ValuesController in hello Web API template.</span></span> <span data-ttu-id="dfef2-139">Deze retourneert Hallo standaardreactie die wordt geleverd door Hallo sjabloon--een JSON-matrix die twee tekenreeksen bevat:</span><span class="sxs-lookup"><span data-stu-id="dfef2-139">It returns hello default response that is provided by hello template--a JSON array that contains two strings:</span></span>
   
    ![Standaardwaarden geretourneerd van ASP.NET Core Web API-sjabloon][browser-aspnet-template-values]
   
    <span data-ttu-id="dfef2-141">Hallo einde van de zelfstudie hello, wordt deze pagina weergegeven Hallo meest recente itemwaarde van onze stateful service in plaats van Hallo standaardtekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="dfef2-141">By hello end of hello tutorial, this page will show hello most recent counter value from our stateful service instead of hello default strings.</span></span>

## <a name="connect-hello-services"></a><span data-ttu-id="dfef2-142">Verbinding maken met de Hallo-services</span><span class="sxs-lookup"><span data-stu-id="dfef2-142">Connect hello services</span></span>
<span data-ttu-id="dfef2-143">Service Fabric biedt volledige flexibiliteit in hoe u met reliable services communiceren.</span><span class="sxs-lookup"><span data-stu-id="dfef2-143">Service Fabric provides complete flexibility in how you communicate with reliable services.</span></span> <span data-ttu-id="dfef2-144">Binnen één toepassing hebt u mogelijk services die toegankelijk zijn via TCP, andere services die toegankelijk via een HTTP REST-API zijn en nog andere services die toegankelijk via het websockets zijn.</span><span class="sxs-lookup"><span data-stu-id="dfef2-144">Within a single application, you might have services that are accessible via TCP, other services that are accessible via an HTTP REST API, and still other services that are accessible via web sockets.</span></span> <span data-ttu-id="dfef2-145">Zie voor achtergrondinformatie over Hallo opties die beschikbaar zijn en Hallo-en nadelen betrokken [services communiceert](service-fabric-connect-and-communicate-with-services.md).</span><span class="sxs-lookup"><span data-stu-id="dfef2-145">For background on hello options available and hello tradeoffs involved, see [Communicating with services](service-fabric-connect-and-communicate-with-services.md).</span></span> <span data-ttu-id="dfef2-146">In deze zelfstudie gebruiken we [Service Fabric-Service voor externe toegang](service-fabric-reliable-services-communication-remoting.md), opgegeven in Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="dfef2-146">In this tutorial, we use [Service Fabric Service Remoting](service-fabric-reliable-services-communication-remoting.md), provided in hello SDK.</span></span>

<span data-ttu-id="dfef2-147">In Hallo Remoting Service benadering (gemodelleerd op externe procedureaanroepen of RPC's), definieert u een tooact interface als openbare contract Hallo voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="dfef2-147">In hello Service Remoting approach (modeled on remote procedure calls or RPCs), you define an interface tooact as hello public contract for hello service.</span></span> <span data-ttu-id="dfef2-148">Vervolgens gebruikt u deze interface toogenerate een proxy-klasse voor interactie met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="dfef2-148">Then, you use that interface toogenerate a proxy class for interacting with hello service.</span></span>

### <a name="create-hello-remoting-interface"></a><span data-ttu-id="dfef2-149">Hallo-interface voor externe toegang maken</span><span class="sxs-lookup"><span data-stu-id="dfef2-149">Create hello remoting interface</span></span>
<span data-ttu-id="dfef2-150">Begint met het maken van Hallo interface tooact als Hallo contract tussen Hallo stateful service en andere services, in deze aanvraag Hallo webproject ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="dfef2-150">Let's start by creating hello interface tooact as hello contract between hello stateful service and other services, in this case hello ASP.NET Core web project.</span></span> <span data-ttu-id="dfef2-151">Deze interface moet worden gedeeld door alle services die gebruikmaken van deze toomake RPC-aanroepen, zodat deze in een eigen Class Library-project maakt.</span><span class="sxs-lookup"><span data-stu-id="dfef2-151">This interface must be shared by all services that use it toomake RPC calls, so we'll create it in its own Class Library project.</span></span>

1. <span data-ttu-id="dfef2-152">Klik in Solution Explorer met de rechtermuisknop op uw oplossing en kies **toevoegen** > **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="dfef2-152">In Solution Explorer, right-click your solution and choose **Add** > **New Project**.</span></span>

2. <span data-ttu-id="dfef2-153">Kies Hallo **Visual C#** vermelding in het navigatiedeelvenster en selecteert u vervolgens Hallo Hallo **Class Library** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="dfef2-153">Choose hello **Visual C#** entry in hello left navigation pane and then select hello **Class Library** template.</span></span> <span data-ttu-id="dfef2-154">Zorg ervoor dat .NET Framework-versie van het Hallo te is ingesteld**4.5.2**.</span><span class="sxs-lookup"><span data-stu-id="dfef2-154">Ensure that hello .NET Framework version is set too**4.5.2**.</span></span>
   
    ![Een project interface voor uw stateful service maken][vs-add-class-library-project]

3. <span data-ttu-id="dfef2-156">Hallo installeren **Microsoft.ServiceFabric.Services.Remoting** NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="dfef2-156">Install hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package.</span></span> <span data-ttu-id="dfef2-157">Zoeken naar **Microsoft.ServiceFabric.Services.Remoting** in Hallo NuGet-pakket manager en installeren voor alle projecten in Hallo oplossing die gebruikmaken van de Service voor externe toegang, waaronder:</span><span class="sxs-lookup"><span data-stu-id="dfef2-157">Search for  **Microsoft.ServiceFabric.Services.Remoting** in hello NuGet package manager and install it for all projects in hello solution that use Service Remoting, including:</span></span>
   - <span data-ttu-id="dfef2-158">Hallo Class Library-project met Hallo service-interface</span><span class="sxs-lookup"><span data-stu-id="dfef2-158">hello Class Library project that contains hello service interface</span></span>
   - <span data-ttu-id="dfef2-159">Hallo Stateful Service-project</span><span class="sxs-lookup"><span data-stu-id="dfef2-159">hello Stateful Service project</span></span>
   - <span data-ttu-id="dfef2-160">Hallo ASP.NET Core web service-project</span><span class="sxs-lookup"><span data-stu-id="dfef2-160">hello ASP.NET Core web service project</span></span>
   
    ![Hallo Services NuGet-pakket toe te voegen][vs-services-nuget-package]

4. <span data-ttu-id="dfef2-162">Maak in klassebibliotheek hello, een interface met een enkele methode `GetCountAsync`, en uit te breiden Hallo-interface van `Microsoft.ServiceFabric.Services.Remoting.IService`.</span><span class="sxs-lookup"><span data-stu-id="dfef2-162">In hello class library, create an interface with a single method, `GetCountAsync`, and extend hello interface from `Microsoft.ServiceFabric.Services.Remoting.IService`.</span></span> <span data-ttu-id="dfef2-163">Hallo remoting interface moet worden afgeleid van deze interface tooindicate is een Service voor externe toegang-interface.</span><span class="sxs-lookup"><span data-stu-id="dfef2-163">hello remoting interface must derive from this interface tooindicate that it is a Service Remoting interface.</span></span>
   
    ```c#
    using Microsoft.ServiceFabric.Services.Remoting;
    using System.Threading.Tasks;
        
    ...

    namespace MyStatefulService.Interface
    {
        public interface ICounter: IService
        {
            Task<long> GetCountAsync();
        }
    }
    ```

### <a name="implement-hello-interface-in-your-stateful-service"></a><span data-ttu-id="dfef2-164">Hallo-interface implementeren in uw stateful service</span><span class="sxs-lookup"><span data-stu-id="dfef2-164">Implement hello interface in your stateful service</span></span>
<span data-ttu-id="dfef2-165">Nu dat we Hallo interface hebt gedefinieerd, moeten we tooimplement in Hallo stateful service.</span><span class="sxs-lookup"><span data-stu-id="dfef2-165">Now that we have defined hello interface, we need tooimplement it in hello stateful service.</span></span>

1. <span data-ttu-id="dfef2-166">In uw stateful service, Voeg een verwijzing toohello klasse bibliotheek-project met Hallo-interface.</span><span class="sxs-lookup"><span data-stu-id="dfef2-166">In your stateful service, add a reference toohello class library project that contains hello interface.</span></span>
   
    ![Een verwijzing toohello class library-project toe te voegen in Hallo stateful service][vs-add-class-library-reference]
2. <span data-ttu-id="dfef2-168">Hallo-klasse die eigenschappen van overneemt vinden `StatefulService`, zoals `MyStatefulService`, en deze uitbreiden tooimplement hello `ICounter` interface.</span><span class="sxs-lookup"><span data-stu-id="dfef2-168">Locate hello class that inherits from `StatefulService`, such as `MyStatefulService`, and extend it tooimplement hello `ICounter` interface.</span></span>
   
    ```c#
    using MyStatefulService.Interface;
   
    ...
   
    public class MyStatefulService : StatefulService, ICounter
    {        
         ...
    }
    ```
3. <span data-ttu-id="dfef2-169">Hallo-één-methode die is gedefinieerd in Hallo nu implementeren `ICounter` interface, `GetCountAsync`.</span><span class="sxs-lookup"><span data-stu-id="dfef2-169">Now implement hello single method that is defined in hello `ICounter` interface, `GetCountAsync`.</span></span>
   
    ```c#
    public async Task<long> GetCountAsync()
    {
        var myDictionary = 
            await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
   
        using (var tx = this.StateManager.CreateTransaction())
        {          
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            return result.HasValue ? result.Value : 0;
        }
    }
    ```

### <a name="expose-hello-stateful-service-using-a-service-remoting-listener"></a><span data-ttu-id="dfef2-170">Hallo stateful service met behulp van een service voor externe toegang-listener blootstelt</span><span class="sxs-lookup"><span data-stu-id="dfef2-170">Expose hello stateful service using a service remoting listener</span></span>
<span data-ttu-id="dfef2-171">Hello `ICounter` interface geïmplementeerd, de laatste stap Hallo is tooopen Hallo Remoting Service communicatiekanaal.</span><span class="sxs-lookup"><span data-stu-id="dfef2-171">With hello `ICounter` interface implemented, hello final step is tooopen hello Service Remoting communication channel.</span></span> <span data-ttu-id="dfef2-172">Voor stateful services, Service Fabric bevat een overschrijfbare methode aangeroepen `CreateServiceReplicaListeners`.</span><span class="sxs-lookup"><span data-stu-id="dfef2-172">For stateful services, Service Fabric provides an overridable method called `CreateServiceReplicaListeners`.</span></span> <span data-ttu-id="dfef2-173">Met deze methode kunt u een of meer communicatielisteners, op basis van Hallo type communicatie dat u voor uw service tooenable wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="dfef2-173">With this method, you can specify one or more communication listeners, based on hello type of communication that you want tooenable for your service.</span></span>

> [!NOTE]
> <span data-ttu-id="dfef2-174">Hallo gelijkwaardige methode voor het openen van een communicatie-kanaal toostateless services heet `CreateServiceInstanceListeners`.</span><span class="sxs-lookup"><span data-stu-id="dfef2-174">hello equivalent method for opening a communication channel toostateless services is called `CreateServiceInstanceListeners`.</span></span>

<span data-ttu-id="dfef2-175">In dit geval wordt de bestaande Hallo `CreateServiceReplicaListeners` methode en geef een exemplaar van `ServiceRemotingListener`, die een RPC-eindpunt maakt die kan worden aangeroepen van clients via `ServiceProxy`.</span><span class="sxs-lookup"><span data-stu-id="dfef2-175">In this case, we replace hello existing `CreateServiceReplicaListeners` method and provide an instance of `ServiceRemotingListener`, which creates an RPC endpoint that is callable from clients through `ServiceProxy`.</span></span>  

<span data-ttu-id="dfef2-176">Hallo `CreateServiceRemotingListener` uitbreidingsmethode op Hallo `IService` interface kunt u tooeasily maken een `ServiceRemotingListener` met alle standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="dfef2-176">hello `CreateServiceRemotingListener` extension method on hello `IService` interface allows you tooeasily create a `ServiceRemotingListener` with all default settings.</span></span> <span data-ttu-id="dfef2-177">toouse deze uitbreidingsmethode, zorg ervoor dat u hebt Hallo `Microsoft.ServiceFabric.Services.Remoting.Runtime` naamruimte geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="dfef2-177">toouse this extension method, ensure you have hello `Microsoft.ServiceFabric.Services.Remoting.Runtime` namespace imported.</span></span> 

```c#
using Microsoft.ServiceFabric.Services.Remoting.Runtime;

...

protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new List<ServiceReplicaListener>()
    {
        new ServiceReplicaListener(
            (context) =>
                this.CreateServiceRemotingListener(context))
    };
}
```


### <a name="use-hello-serviceproxy-class-toointeract-with-hello-service"></a><span data-ttu-id="dfef2-178">Hallo ServiceProxy klasse toointeract gebruiken met Hallo-service</span><span class="sxs-lookup"><span data-stu-id="dfef2-178">Use hello ServiceProxy class toointeract with hello service</span></span>
<span data-ttu-id="dfef2-179">Onze stateful service is nu gereed tooreceive verkeer van andere services via RPC.</span><span class="sxs-lookup"><span data-stu-id="dfef2-179">Our stateful service is now ready tooreceive traffic from other services over RPC.</span></span> <span data-ttu-id="dfef2-180">Blijft is zodat Hallo code toocommunicate met het toevoegen van Hallo ASP.NET-webservice.</span><span class="sxs-lookup"><span data-stu-id="dfef2-180">So all that remains is adding hello code toocommunicate with it from hello ASP.NET web service.</span></span>

1. <span data-ttu-id="dfef2-181">Toevoegen in uw ASP.NET-project een verwijzing toohello class-bibliotheek met Hallo `ICounter` interface.</span><span class="sxs-lookup"><span data-stu-id="dfef2-181">In your ASP.NET project, add a reference toohello class library that contains hello `ICounter` interface.</span></span>

2. <span data-ttu-id="dfef2-182">Eerder u Hallo toegevoegd **Microsoft.ServiceFabric.Services.Remoting** NuGet-pakket toohello ASP.NET-project.</span><span class="sxs-lookup"><span data-stu-id="dfef2-182">Earlier you added hello **Microsoft.ServiceFabric.Services.Remoting** NuGet package toohello ASP.NET project.</span></span> <span data-ttu-id="dfef2-183">Dit pakket biedt Hallo `ServiceProxy` klasse die u gebruikt toomake RPC toohello stateful service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="dfef2-183">This package provides hello `ServiceProxy` class which you use toomake RPC calls toohello stateful service.</span></span> <span data-ttu-id="dfef2-184">Zorg ervoor dat deze NuGet-pakket is geïnstalleerd in Hallo ASP.NET Core web service-project.</span><span class="sxs-lookup"><span data-stu-id="dfef2-184">Ensure this NuGet package is installed in hello ASP.NET Core web service project.</span></span>

4. <span data-ttu-id="dfef2-185">In Hallo **domeincontrollers** map, open Hallo `ValuesController` klasse.</span><span class="sxs-lookup"><span data-stu-id="dfef2-185">In hello **Controllers** folder, open hello `ValuesController` class.</span></span> <span data-ttu-id="dfef2-186">Houd er rekening mee dat Hallo `Get` methode wordt momenteel alleen een vastgelegde tekenreeksmatrix van 'waarde1' en 'waarde2'--die overeenkomt met wat we eerder in de browser Hallo gezien.</span><span class="sxs-lookup"><span data-stu-id="dfef2-186">Note that hello `Get` method currently just returns a hard-coded string array of "value1" and "value2"--which matches what we saw earlier in hello browser.</span></span> <span data-ttu-id="dfef2-187">Vervang deze implementatie met Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="dfef2-187">Replace this implementation with hello following code:</span></span>
   
    ```c#
    using MyStatefulService.Interface;
    using Microsoft.ServiceFabric.Services.Client;
    using Microsoft.ServiceFabric.Services.Remoting.Client;
   
    ...

    [HttpGet]
    public async Task<IEnumerable<string>> Get()
    {
        ICounter counter =
            ServiceProxy.Create<ICounter>(new Uri("fabric:/MyApplication/MyStatefulService"), new ServicePartitionKey(0));
   
        long count = await counter.GetCountAsync();
   
        return new string[] { count.ToString() };
    }
    ```
   
    <span data-ttu-id="dfef2-188">de eerste coderegel Hallo is Hallo sleutel.</span><span class="sxs-lookup"><span data-stu-id="dfef2-188">hello first line of code is hello key one.</span></span> <span data-ttu-id="dfef2-189">toocreate hello ICounter proxy toohello stateful service, moet u twee soorten informatie tooprovide: een partitie-ID en het Hallo-naam van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="dfef2-189">toocreate hello ICounter proxy toohello stateful service, you need tooprovide two pieces of information: a partition ID and hello name of hello service.</span></span>
   
    <span data-ttu-id="dfef2-190">U kunt partitionering tooscale stateful services door deze van hun status in verschillende buckets, op basis van een sleutel die u hebt gedefinieerd, zoals een klant-ID of postcode te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dfef2-190">You can use partitioning tooscale stateful services by breaking up their state into different buckets, based on a key that you define, such as a customer ID or postal code.</span></span> <span data-ttu-id="dfef2-191">In onze toepassing trivial heeft Hallo stateful service slechts één partitie zodat Hallo-sleutel is niet van belang.</span><span class="sxs-lookup"><span data-stu-id="dfef2-191">In our trivial application, hello stateful service only has one partition, so hello key doesn't matter.</span></span> <span data-ttu-id="dfef2-192">Een sleutel die u opgeeft leidt toohello dezelfde partitie.</span><span class="sxs-lookup"><span data-stu-id="dfef2-192">Any key that you provide will lead toohello same partition.</span></span> <span data-ttu-id="dfef2-193">toolearn meer informatie over het partitioneren van services, Zie [hoe toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="dfef2-193">toolearn more about partitioning services, see [How toopartition Service Fabric Reliable Services](service-fabric-concepts-partitioning.md).</span></span>
   
    <span data-ttu-id="dfef2-194">Hallo-servicenaam is een URI van Hallo formulier fabric: /&lt;$application_name&gt;/&lt;service_name&gt;.</span><span class="sxs-lookup"><span data-stu-id="dfef2-194">hello service name is a URI of hello form fabric:/&lt;application_name&gt;/&lt;service_name&gt;.</span></span>
   
    <span data-ttu-id="dfef2-195">Met deze twee soorten informatie kunt Service Fabric Hallo-machine die aanvragen moeten worden verzonden naar een unieke identificatie.</span><span class="sxs-lookup"><span data-stu-id="dfef2-195">With these two pieces of information, Service Fabric can uniquely identify hello machine that requests should be sent to.</span></span> <span data-ttu-id="dfef2-196">Hallo `ServiceProxy` klasse ook naadloos verwerkt Hallo geval waarbij Hallo-machine die als host fungeert voor Hallo stateful service partitie is mislukt en een andere computer moet worden bevorderd tootake plaats.</span><span class="sxs-lookup"><span data-stu-id="dfef2-196">hello `ServiceProxy` class also seamlessly handles hello case where hello machine that hosts hello stateful service partition fails and another machine must be promoted tootake its place.</span></span> <span data-ttu-id="dfef2-197">Deze abstractie maakt schrijven Hallo van client code toodeal met andere services die aanzienlijk eenvoudiger.</span><span class="sxs-lookup"><span data-stu-id="dfef2-197">This abstraction makes writing hello client code toodeal with other services significantly simpler.</span></span>
   
    <span data-ttu-id="dfef2-198">Wanneer we Hallo proxy hebt, roepen we Hallo `GetCountAsync` methode en het resultaat te retourneren.</span><span class="sxs-lookup"><span data-stu-id="dfef2-198">Once we have hello proxy, we simply invoke hello `GetCountAsync` method and return its result.</span></span>

5. <span data-ttu-id="dfef2-199">Druk op F5 opnieuw toorun Hallo toepassing gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="dfef2-199">Press F5 again toorun hello modified application.</span></span> <span data-ttu-id="dfef2-200">Als voordat, Visual Studio wordt automatisch gestart Hallo browser toohello hoofdmap van Hallo webproject.</span><span class="sxs-lookup"><span data-stu-id="dfef2-200">As before, Visual Studio automatically launches hello browser toohello root of hello web project.</span></span> <span data-ttu-id="dfef2-201">Hallo 'api en-waarden' pad toevoegen en u ziet Hallo huidige waarde van het prestatiemeteritem geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="dfef2-201">Add hello "api/values" path, and you should see hello current counter value returned.</span></span>
   
    ![Hallo stateful itemwaarde weergegeven in de browser Hallo][browser-aspnet-counter-value]
   
    <span data-ttu-id="dfef2-203">Vernieuw de browser Hallo periodiek toosee Hallo teller waarde update.</span><span class="sxs-lookup"><span data-stu-id="dfef2-203">Refresh hello browser periodically toosee hello counter value update.</span></span>

## <a name="kestrel-and-weblistener"></a><span data-ttu-id="dfef2-204">Kestrel en WebListener</span><span class="sxs-lookup"><span data-stu-id="dfef2-204">Kestrel and WebListener</span></span>

<span data-ttu-id="dfef2-205">Hallo standaard ASP.NET Core-webserver, Kestrel, ook wel is [momenteel niet ondersteund voor het verwerken van directe internetverkeer](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span><span class="sxs-lookup"><span data-stu-id="dfef2-205">hello default ASP.NET Core web server, known as Kestrel, is [not currently supported for handling direct internet traffic](https://docs.microsoft.com/aspnet/core/fundamentals/servers/kestrel).</span></span> <span data-ttu-id="dfef2-206">Als gevolg hiervan hello ASP.NET Core staatloze servicesjabloon voor Service Fabric gebruikt [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) standaard.</span><span class="sxs-lookup"><span data-stu-id="dfef2-206">As a result, hello ASP.NET Core stateless service template for Service Fabric uses [WebListener](https://docs.microsoft.com/aspnet/core/fundamentals/servers/weblistener) by default.</span></span> 

<span data-ttu-id="dfef2-207">toolearn meer informatie over Kestrel en WebListener in Service Fabric-services, Raadpleeg te[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span><span class="sxs-lookup"><span data-stu-id="dfef2-207">toolearn more about Kestrel and WebListener in Service Fabric services, please refer too[ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md).</span></span>

## <a name="connecting-tooa-reliable-actor-service"></a><span data-ttu-id="dfef2-208">Verbinding maken met tooa betrouwbare Actor-service</span><span class="sxs-lookup"><span data-stu-id="dfef2-208">Connecting tooa Reliable Actor service</span></span>
<span data-ttu-id="dfef2-209">Deze zelfstudie is gericht op het toevoegen van een webfront-end die gecommuniceerd met een stateful service.</span><span class="sxs-lookup"><span data-stu-id="dfef2-209">This tutorial focused on adding a web front end that communicated with a stateful service.</span></span> <span data-ttu-id="dfef2-210">U kunt echter een vergelijkbaar model tootalk tooactors volgen.</span><span class="sxs-lookup"><span data-stu-id="dfef2-210">However, you can follow a very similar model tootalk tooactors.</span></span> <span data-ttu-id="dfef2-211">Wanneer u een betrouwbare Actor-project maakt, wordt in Visual Studio automatisch een interface-project voor u gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="dfef2-211">When you create a Reliable Actor project, Visual Studio automatically generates an interface project for you.</span></span> <span data-ttu-id="dfef2-212">Kunt u deze interface toogenerate een actor-proxy in Hallo web project toocommunicate met acteur Hallo.</span><span class="sxs-lookup"><span data-stu-id="dfef2-212">You can use that interface toogenerate an actor proxy in hello web project toocommunicate with hello actor.</span></span> <span data-ttu-id="dfef2-213">Hallo communicatiekanaal is automatisch beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="dfef2-213">hello communication channel is provided automatically.</span></span> <span data-ttu-id="dfef2-214">Zo hoeft u geen toodo alles dat gelijkwaardige tooestablishing is een `ServiceRemotingListener` net zoals voor stateful service Hallo in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="dfef2-214">So you do not need toodo anything that is equivalent tooestablishing a `ServiceRemotingListener` like you did for hello stateful service in this tutorial.</span></span>

## <a name="how-web-services-work-on-your-local-cluster"></a><span data-ttu-id="dfef2-215">De werking van web-services op uw lokale cluster</span><span class="sxs-lookup"><span data-stu-id="dfef2-215">How web services work on your local cluster</span></span>
<span data-ttu-id="dfef2-216">U kunt precies Hallo dezelfde Service Fabric-toepassing tooa meerdere machine cluster die u hebt geïmplementeerd op uw lokale cluster en maximaal vertrouwen werkt zoals verwacht in het algemeen kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="dfef2-216">In general, you can deploy exactly hello same Service Fabric application tooa multi-machine cluster that you deployed on your local cluster and be highly confident that it works as you expect.</span></span> <span data-ttu-id="dfef2-217">Dit is omdat uw lokale cluster is gewoon een vijf knooppunten configuratie die is samengevouwen tooa enkele machine.</span><span class="sxs-lookup"><span data-stu-id="dfef2-217">This is because your local cluster is simply a five-node configuration that is collapsed tooa single machine.</span></span>

<span data-ttu-id="dfef2-218">Wanneer er tooweb services, maar is er een belangrijke aspect.</span><span class="sxs-lookup"><span data-stu-id="dfef2-218">When it comes tooweb services, however, there is one key nuance.</span></span> <span data-ttu-id="dfef2-219">Als uw cluster zich achter een load balancer, zoals dat in Azure, moet u ervoor zorgen dat uw webservices zijn geïmplementeerd op elke machine sinds Hallo load balancer gewoon round robins verkeer over Hallo-machines.</span><span class="sxs-lookup"><span data-stu-id="dfef2-219">When your cluster sits behind a load balancer, as it does in Azure, you must ensure that your web services are deployed on every machine since hello load balancer simply round-robins traffic across hello machines.</span></span> <span data-ttu-id="dfef2-220">U kunt dit doen door de instelling Hallo `InstanceCount` voor Hallo service toohello speciale waarde '1'.</span><span class="sxs-lookup"><span data-stu-id="dfef2-220">You can do this by setting hello `InstanceCount` for hello service toohello special value of "-1".</span></span>

<span data-ttu-id="dfef2-221">Daarentegen, wanneer u een webservice lokaal uitvoeren, moet u tooensure dat slechts één exemplaar van Hallo-service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dfef2-221">By contrast, when you run a web service locally, you need tooensure that only one instance of hello service is running.</span></span> <span data-ttu-id="dfef2-222">Anders u uitvoeren in conflicten uit meerdere processen die op Hallo hetzelfde luisteren pad en de poort.</span><span class="sxs-lookup"><span data-stu-id="dfef2-222">Otherwise, you run into conflicts from multiple processes that are listening on hello same path and port.</span></span> <span data-ttu-id="dfef2-223">Als gevolg hiervan Hallo web service-exemplaren te moet worden ingesteld '1' voor lokale implementaties.</span><span class="sxs-lookup"><span data-stu-id="dfef2-223">As a result, hello web service instance count should be set too"1" for local deployments.</span></span>

<span data-ttu-id="dfef2-224">hoe tooconfigure verschillende waarden voor verschillende omgeving zien toolearn [beheren voor omgevingen met meerdere parameters voor de toepassing](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="dfef2-224">toolearn how tooconfigure different values for different environment, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfef2-225">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dfef2-225">Next steps</span></span>
<span data-ttu-id="dfef2-226">Nu dat u een web-front end set hebt voor uw toepassing met ASP.NET Core, meer informatie over [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) voor een diepgaand inzicht in hoe ASP.NET Core met Service Fabric werkt.</span><span class="sxs-lookup"><span data-stu-id="dfef2-226">Now that you have a web front end set up for your application with ASP.NET Core, learn more about [ASP.NET Core in Service Fabric Reliable Services](service-fabric-reliable-services-communication-aspnetcore.md) for an in-depth understanding of how ASP.NET Core works with Service Fabric.</span></span>

<span data-ttu-id="dfef2-227">Vervolgens [meer informatie over de communicatie met services](service-fabric-connect-and-communicate-with-services.md) in het algemeen tooget een volledige afbeelding van hoe service communicatie werkt in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="dfef2-227">Next, [learn more about communicating with services](service-fabric-connect-and-communicate-with-services.md) in general tooget a complete picture of how service communication works in Service Fabric.</span></span>

<span data-ttu-id="dfef2-228">Zodra u een goed inzicht hebt in hoe servicecommunicatie werkt, [een cluster in Azure maken en implementeren van uw toepassing toohello cloud](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dfef2-228">Once you have a good understanding of how service communication works, [create a cluster in Azure and deploy your application toohello cloud](service-fabric-cluster-creation-via-portal.md).</span></span>

<!-- Image References -->

[vs-add-new-service]: ./media/service-fabric-add-a-web-frontend/vs-add-new-service.png
[vs-new-service-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-service-dialog.png
[vs-new-aspnet-project-dialog]: ./media/service-fabric-add-a-web-frontend/vs-new-aspnet-project-dialog.png
[browser-aspnet-template-values]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-template-values.png
[vs-add-class-library-project]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-project.png
[vs-add-class-library-reference]: ./media/service-fabric-add-a-web-frontend/vs-add-class-library-reference.png
[vs-services-nuget-package]: ./media/service-fabric-add-a-web-frontend/vs-services-nuget-package.png
[browser-aspnet-counter-value]: ./media/service-fabric-add-a-web-frontend/browser-aspnet-counter-value.png
[vs-create-platform]: ./media/service-fabric-add-a-web-frontend/vs-create-platform.png


<!-- external links -->
[dotnetcore-install]: https://www.microsoft.com/net/core#windows

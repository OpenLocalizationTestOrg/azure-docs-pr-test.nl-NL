---
title: aaaGet slag met API-Apps en ASP.NET in App Service | Microsoft Docs
description: Ontdek hoe toocreate, implementeren en gebruiken van een ASP.NET API-app in Azure App Service met behulp van Visual Studio 2015.
services: app-service\api
documentationcenter: .net
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: ddc028b2-cde0-4567-a6ee-32cb264a830a
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: hero-article
ms.date: 09/20/2016
ms.author: alkarche
ms.openlocfilehash: d3e90f1585907d183b0435c6cafc5585bc1e29ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="092c1-103">Aan de slag met API-apps, ASP.NET en Swagger in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="092c1-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="092c1-104">Dit is Hallo eerst in een reeks zelfstudies die laten zien hoe toouse functies van Azure App Service die zijn handig voor het ontwikkelen en hosten van RESTful-API's.</span><span class="sxs-lookup"><span data-stu-id="092c1-104">This is hello first in a series of tutorials that show how toouse features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="092c1-105">In deze zelfstudie wordt ondersteuning voor API-metagegevens in Swagger-indeling besproken.</span><span class="sxs-lookup"><span data-stu-id="092c1-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="092c1-106">U leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="092c1-106">You'll learn:</span></span>

* <span data-ttu-id="092c1-107">Hoe toocreate en implementeren van [API-apps](app-service-api-apps-why-best-platform.md) in Azure App Service met behulp van hulpprogramma's die zijn ingebouwd in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="092c1-107">How toocreate and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="092c1-108">Hoe tooautomate API-detectie met behulp van Hallo Swashbuckle NuGet-pakket genereren toodynamically Swagger API-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="092c1-108">How tooautomate API discovery by using hello Swashbuckle NuGet package toodynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="092c1-109">Hoe toouse Swagger API-metagegevens tooautomatically clientcode genereren voor een API-app.</span><span class="sxs-lookup"><span data-stu-id="092c1-109">How toouse Swagger API metadata tooautomatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="092c1-110">Overzicht van voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="092c1-110">Sample application overview</span></span>
<span data-ttu-id="092c1-111">In deze zelfstudie werkt u met een voorbeeld van een eenvoudige takenlijsttoepassing.</span><span class="sxs-lookup"><span data-stu-id="092c1-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="092c1-112">Hallo-toepassing heeft een front-end van één pagina (SPA application '), een ASP.NET Web API als middelste laag en een ASP.NET Web API als gegevenslaag.</span><span class="sxs-lookup"><span data-stu-id="092c1-112">hello application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![Diagram van API-apps-voorbeeldtoepassing](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="092c1-114">Hier volgt een schermopname van het Hallo [AngularJS](https://angularjs.org/) front-end.</span><span class="sxs-lookup"><span data-stu-id="092c1-114">Here's a screen shot of hello [AngularJS](https://angularjs.org/) front end.</span></span>

![Lijst met toepassingen toodo en API Apps-voorbeeld](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="092c1-116">Hallo Visual Studio-oplossing omvat drie projecten:</span><span class="sxs-lookup"><span data-stu-id="092c1-116">hello Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="092c1-117">**ToDoListAngular** -Hallo-front-end: een AngularJS SPA die Hallo middelste laag aanroept.</span><span class="sxs-lookup"><span data-stu-id="092c1-117">**ToDoListAngular** - hello front end: an AngularJS SPA that calls hello middle tier.</span></span>
* <span data-ttu-id="092c1-118">**ToDoListAPI** -Hallo middelste laag: een ASP.NET Web API-project die Hallo gegevenslaag tooperform CRUD-bewerkingen op taken aanroept.</span><span class="sxs-lookup"><span data-stu-id="092c1-118">**ToDoListAPI** - hello middle tier: an ASP.NET Web API project that calls hello data tier tooperform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="092c1-119">**ToDoListDataAPI** -Hallo gegevenslaag: een ASP.NET Web API-project dat CRUD-bewerkingen op taken uitvoert.</span><span class="sxs-lookup"><span data-stu-id="092c1-119">**ToDoListDataAPI** - hello data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="092c1-120">Hallo architectuur met drie lagen is een van de vele architecturen die u kunt implementeren met behulp van API Apps en wordt hier alleen voor demonstratiedoeleinden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="092c1-120">hello three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="092c1-121">Hallo-code in elke laag is net zo eenvoudig als mogelijke toodemonstrate API Apps-functies. Hallo gegevenslaag gebruikt bijvoorbeeld geheugen van de server in plaats van een database als het mechanisme voor persistentie.</span><span class="sxs-lookup"><span data-stu-id="092c1-121">hello code in each tier is as simple as possible toodemonstrate API Apps features; for example, hello data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="092c1-122">Op het voltooien van deze zelfstudie hebt u Hallo twee Web API-projecten en uitgevoerd in de cloud Hallo in App Service API-apps.</span><span class="sxs-lookup"><span data-stu-id="092c1-122">On completing this tutorial, you'll have hello two Web API projects up and running in hello cloud in App Service API apps.</span></span>

<span data-ttu-id="092c1-123">Hallo volgende zelfstudie in de reeks Hallo implementeert Hallo SPA-front-end toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="092c1-123">hello next tutorial in hello series deploys hello SPA front end toohello cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="092c1-124">Vereisten</span><span class="sxs-lookup"><span data-stu-id="092c1-124">Prerequisites</span></span>
* <span data-ttu-id="092c1-125">ASP.NET Web API - instructies Hallo-zelfstudie wordt ervan uitgegaan dat u een elementaire kennis hebben van hoe toowork met ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="092c1-125">ASP.NET Web API - hello tutorial instructions assume you have a basic knowledge of how toowork with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="092c1-126">Azure-account: u kunt [een gratis Azure-account openen](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="092c1-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="092c1-127">Als u wilt dat tooget gestart met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="092c1-127">If you want tooget started with Azure App Service before you sign up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="092c1-128">Daar kunt u direct een eenvoudige, tijdelijke app maken in App Service. U hebt hiervoor **geen creditcard nodig** en bent nergens toe verplicht.</span><span class="sxs-lookup"><span data-stu-id="092c1-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="092c1-129">Visual Studio 2015 met de Hallo [Azure SDK voor .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) -Hallo SDK installeert Visual Studio 2015 automatisch als u nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="092c1-129">Visual Studio 2015 with hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - hello SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="092c1-130">Klik in Visual Studio op Help -> Over Microsoft Visual Studio en zorg ervoor dat 'Azure App Service Tools v2.9.1' of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="092c1-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Versie van Azure App Tools](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="092c1-132">Afhankelijk van hoeveel van Hallo SDK-afhankelijkheden u al op uw computer hebt, kan installeren Hallo SDK lang duren, van enkele minuten tooa halfuur of meer.</span><span class="sxs-lookup"><span data-stu-id="092c1-132">Depending on how many of hello SDK dependencies you already have on your machine, installing hello SDK could take a long time, from several minutes tooa half hour or more.</span></span>
    > 
    > 

## <a name="download-hello-sample-application"></a><span data-ttu-id="092c1-133">Hallo-voorbeeldtoepassing downloaden</span><span class="sxs-lookup"><span data-stu-id="092c1-133">Download hello sample application</span></span>
1. <span data-ttu-id="092c1-134">Hallo downloaden [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="092c1-134">Download hello [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="092c1-135">U kunt klikken op Hallo **ZIP downloaden** knop of kloon Hallo-opslagplaats op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="092c1-135">You can click hello **Download ZIP** button or clone hello repository on your local machine.</span></span>
2. <span data-ttu-id="092c1-136">Open de ToDoList-oplossing Hallo in Visual Studio 2015 of 2013.</span><span class="sxs-lookup"><span data-stu-id="092c1-136">Open hello ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="092c1-137">U moet tootrust elke oplossing.</span><span class="sxs-lookup"><span data-stu-id="092c1-137">You will need tootrust each solution.</span></span>
         <span data-ttu-id="092c1-138">![Beveiligingswaarschuwing](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="092c1-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="092c1-139">Hallo-oplossing (CTRL + SHIFT + B) toorestore hello NuGet-pakketten maken.</span><span class="sxs-lookup"><span data-stu-id="092c1-139">Build hello solution (CTRL + SHIFT + B)  toorestore hello NuGet packages.</span></span>
   
    <span data-ttu-id="092c1-140">Als u toosee Hallo toepassing in bewerking wilt voordat u deze implementeert, kunt u deze lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="092c1-140">If you want toosee hello application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="092c1-141">Zorg ervoor dat de ToDoListDataAPI uw opstartproject en Voer Hallo-oplossing is.</span><span class="sxs-lookup"><span data-stu-id="092c1-141">Make sure that ToDoListDataAPI is your startup project and run hello solution.</span></span> <span data-ttu-id="092c1-142">Verwachte toosee 403 HTTP-fout in uw browser.</span><span class="sxs-lookup"><span data-stu-id="092c1-142">You should expect toosee a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="092c1-143">Swagger API-metagegevens en -gebruikersinterface gebruiken</span><span class="sxs-lookup"><span data-stu-id="092c1-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="092c1-144">Ondersteuning voor [Swagger](http://swagger.io/) 2.0 API-metagegevens is ingebouwd in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="092c1-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="092c1-145">Elke API-app kunt een URL-eindpunt dat metagegevens voor Hallo API in Swagger JSON-indeling retourneert opgeven.</span><span class="sxs-lookup"><span data-stu-id="092c1-145">Each API app can specify a URL endpoint that returns metadata for hello API in Swagger JSON format.</span></span> <span data-ttu-id="092c1-146">Hallo metagegevens geretourneerd vanuit dat eindpunt mag toogenerate clientcode gebruikt.</span><span class="sxs-lookup"><span data-stu-id="092c1-146">hello metadata returned from that endpoint can be used toogenerate client code.</span></span>

<span data-ttu-id="092c1-147">Een ASP.NET Web API-project kan Swagger-metagegevens dynamisch genereren met behulp van Hallo [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="092c1-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using hello [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="092c1-148">Hallo Swashbuckle NuGet-pakket is al geïnstalleerd in Hallo ToDoListDataAPI- en ToDoListAPI-projecten die u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="092c1-148">hello Swashbuckle NuGet package is already installed in hello ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="092c1-149">In deze sectie van de zelfstudie Hallo u bekijkt hello gegenereerde Swagger 2.0-metagegevens en probeert u een testgebruikersinterface die is gebaseerd op Hallo Swagger-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="092c1-149">In this section of hello tutorial, you look at hello generated Swagger 2.0 metadata, and then you try out a test UI that is based on hello Swagger metadata.</span></span>

1. <span data-ttu-id="092c1-150">Hallo ToDoListDataAPI project instellen (**niet** hello ToDoListAPI-project) als opstartproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="092c1-150">Set hello ToDoListDataAPI project (**not** hello ToDoListAPI project) as hello startup project.</span></span>
   
    ![ToDoDataAPI instellen als opstartproject](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="092c1-152">Druk op F5 of klik op **fouten opsporen > Foutopsporing starten** toorun Hallo-project in de foutopsporingsmodus.</span><span class="sxs-lookup"><span data-stu-id="092c1-152">Press F5 or click **Debug > Start Debugging** toorun hello project in debug mode.</span></span>
   
    <span data-ttu-id="092c1-153">Hallo-browser wordt geopend en ziet u Hallo HTTP 403-foutpagina.</span><span class="sxs-lookup"><span data-stu-id="092c1-153">hello browser opens and shows hello HTTP 403 error page.</span></span>
3. <span data-ttu-id="092c1-154">Voeg in de adresbalk van uw browser `swagger/docs/v1` toohello einde van het Hallo-regel en druk vervolgens op ENTER.</span><span class="sxs-lookup"><span data-stu-id="092c1-154">In your browser address bar, add `swagger/docs/v1` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="092c1-155">(Hallo-URL is `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="092c1-155">(hello URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="092c1-156">Dit is standaard-URL Hallo door Swashbuckle tooreturn Swagger 2.0 JSON-metagegevens gebruikt voor Hallo API.</span><span class="sxs-lookup"><span data-stu-id="092c1-156">This is hello default URL used by Swashbuckle tooreturn Swagger 2.0 JSON metadata for hello API.</span></span>
   
    <span data-ttu-id="092c1-157">Als u van Internet Explorer gebruikmaakt, Hallo browser wordt u gevraagd toodownload een *v1.json* bestand.</span><span class="sxs-lookup"><span data-stu-id="092c1-157">If you're using Internet Explorer, hello browser prompts you toodownload a *v1.json* file.</span></span>
   
    ![JSON-metagegevens downloaden in Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="092c1-159">Als u Chrome, Firefox of Edge gebruikt, wordt in Hallo browser Hallo JSON in Hallo browservenster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="092c1-159">If you're using Chrome, Firefox, or Edge, hello browser displays hello JSON in hello browser window.</span></span> <span data-ttu-id="092c1-160">Verschillende browsers verwerken JSON anders en uw browservenster mag niet precies hetzelfde uitzien als Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="092c1-160">Different browsers handle JSON differently, and your browser window may not look exactly like hello example.</span></span>
   
    ![JSON-metagegevens in Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="092c1-162">Hallo volgende voorbeeld toont de eerste sectie Hallo van Hallo Swagger-metagegevens voor Hallo-API met Hallo definitie voor Hallo methode Get.</span><span class="sxs-lookup"><span data-stu-id="092c1-162">hello following sample shows hello first section of hello Swagger metadata for hello API, with hello definition for hello Get method.</span></span> <span data-ttu-id="092c1-163">Deze metagegevens is welke stations Hallo Swagger-gebruikersinterface die u in de volgende stappen uit Hallo gebruikt, en u deze in een volgende sectie van de zelfstudie tooautomatically Hallo gebruiken genereren van clientcode.</span><span class="sxs-lookup"><span data-stu-id="092c1-163">This metadata is what drives hello Swagger UI that you use in hello following steps, and you use it in a later section of hello tutorial tooautomatically generate client code.</span></span>
   
        {
          "swagger": "2.0",
          "info": {
            "version": "v1",
            "title": "ToDoListDataAPI"
          },
          "host": "localhost:45914",
          "schemes": [ "http" ],
          "paths": {
            "/api/ToDoList": {
              "get": {
                "tags": [ "ToDoList" ],
                "operationId": "ToDoList_GetByOwner",
                "consumes": [ ],
                "produces": [ "application/json", "text/json", "application/xml", "text/xml" ],
                "parameters": [
                  {
                    "name": "owner",
                    "in": "query",
                    "required": true,
                    "type": "string"
                  }
                ],
                "responses": {
                  "200": {
                    "description": "OK",
                    "schema": {
                      "type": "array",
                      "items": { "$ref": "#/definitions/ToDoItem" }
                    }
                  }
                },
                "deprecated": false
              },
4. <span data-ttu-id="092c1-164">Sluit Hallo browser en stop de foutopsporing van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="092c1-164">Close hello browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="092c1-165">Project in Hallo ToDoListDataAPI in **Solution Explorer**Open Hallo *App_Start\SwaggerConfig.cs* file en schuif omlaag tooline 174 en het commentaar verwijderen Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="092c1-165">In hello ToDoListDataAPI project in **Solution Explorer**, open hello *App_Start\SwaggerConfig.cs* file, then scroll down tooline 174 and uncomment hello following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="092c1-166">Hallo *SwaggerConfig.cs* bestand wordt gemaakt wanneer u Hallo Swashbuckle-pakket in een project installeert.</span><span class="sxs-lookup"><span data-stu-id="092c1-166">hello *SwaggerConfig.cs* file is created when you install hello Swashbuckle package in a project.</span></span> <span data-ttu-id="092c1-167">Hallo-bestand bevat een aantal manieren tooconfigure Swashbuckle.</span><span class="sxs-lookup"><span data-stu-id="092c1-167">hello file provides a number of ways tooconfigure Swashbuckle.</span></span>
   
    <span data-ttu-id="092c1-168">Hallo-code u hebt zonder opmerkingen schakelt Hallo Swagger-gebruikersinterface die u gebruikt in hello te volgen stappen.</span><span class="sxs-lookup"><span data-stu-id="092c1-168">hello code you've uncommented enables hello Swagger UI that you use in hello following steps.</span></span> <span data-ttu-id="092c1-169">Wanneer u een Web API-project maakt met behulp van Hallo API-app-projectsjabloon, wordt deze code standaard uitgecommentarieerd als veiligheidsmaatregel.</span><span class="sxs-lookup"><span data-stu-id="092c1-169">When you create a Web API project by using hello API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="092c1-170">Hallo-project opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="092c1-170">Run hello project again.</span></span>
7. <span data-ttu-id="092c1-171">Voeg in de adresbalk van uw browser `swagger` toohello einde van het Hallo-regel en druk vervolgens op ENTER.</span><span class="sxs-lookup"><span data-stu-id="092c1-171">In your browser address bar, add `swagger` toohello end of hello line, and then press Return.</span></span> <span data-ttu-id="092c1-172">(Hallo-URL is `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="092c1-172">(hello URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="092c1-173">Wanneer Hallo Swagger-gebruikersinterface pagina wordt weergegeven, klikt u op **ToDoList** toosee Hallo methoden beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="092c1-173">When hello Swagger UI page appears, click **ToDoList** toosee hello methods available.</span></span>
   
    ![Beschikbare methoden in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="092c1-175">Klik eerst op Hallo **ophalen** knop in Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="092c1-175">Click hello first **Get** button in hello list.</span></span>
10. <span data-ttu-id="092c1-176">In Hallo **Parameters** sectie, geeft u een sterretje als waarde Hallo Hallo `owner` parameter en klik vervolgens op **Try it out in**.</span><span class="sxs-lookup"><span data-stu-id="092c1-176">In hello **Parameters** section, enter an asterisk as hello value of hello `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="092c1-177">Wanneer u verificatie in latere zelfstudies toevoegt, geven de middelste laag Hallo toohello gegevenslaag voor Hallo werkelijke gebruikers-ID.</span><span class="sxs-lookup"><span data-stu-id="092c1-177">When you add authentication in later tutorials, hello middle tier will provide hello actual user ID toohello data tier.</span></span> <span data-ttu-id="092c1-178">Nu alle taken een sterretje als eigenaar-ID tijdens het Hallo-toepassing wordt uitgevoerd zonder verificatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="092c1-178">For now, all tasks will have asterisk as their owner ID while hello application runs without authentication enabled.</span></span>
    
    ![Try it out in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="092c1-180">Hallo Swagger-gebruikersinterface roept Hallo ToDoList Get-methode en Hallo responscode en JSON-resultaten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="092c1-180">hello Swagger UI calls hello ToDoList Get method and displays hello response code and JSON results.</span></span>
    
    ![Resultaten van Try it out in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="092c1-182">Klik op **Post**, en klik vervolgens op Hallo vak onder **modelschema**.</span><span class="sxs-lookup"><span data-stu-id="092c1-182">Click **Post**, and then click hello box under **Model Schema**.</span></span>
    
    <span data-ttu-id="092c1-183">Als u op Hallo model schema prefills Hallo invoervak waarin u de parameterwaarde Hallo voor Hallo Post-methode kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="092c1-183">Clicking hello model schema prefills hello input box where you can specify hello parameter value for hello Post method.</span></span> <span data-ttu-id="092c1-184">(Als dit niet in Internet Explorer werkt, een andere browser gebruikt of Hallo parameterwaarde handmatig invoeren in de volgende stap Hallo.)</span><span class="sxs-lookup"><span data-stu-id="092c1-184">(If this doesn't work in Internet Explorer, use a different browser or enter hello parameter value manually in hello next step.)</span></span>  
    
    ![Post voor Try it out in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="092c1-186">Wijziging Hallo JSON in Hallo `todo` parameter invoer vak zodat het lijkt erop dat Hallo volgende voorbeeld of vervang deze door uw eigen beschrijvende tekst:</span><span class="sxs-lookup"><span data-stu-id="092c1-186">Change hello JSON in hello `todo` parameter input box so that it looks like hello following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy hello dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="092c1-187">Klik op **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="092c1-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="092c1-188">Hallo ToDoList-API retourneert een 204 HTTP-antwoordcode die slagen aangeeft.</span><span class="sxs-lookup"><span data-stu-id="092c1-188">hello ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="092c1-189">Klik eerst op Hallo **ophalen** knop en klik vervolgens in die sectie van de pagina Hallo op Hallo **Try it out in** knop.</span><span class="sxs-lookup"><span data-stu-id="092c1-189">Click hello first **Get** button, and then in that section of hello page click hello **Try it out** button.</span></span>
    
    <span data-ttu-id="092c1-190">Hallo antwoord van Get-methode bevat nu Hallo nieuw toodo item.</span><span class="sxs-lookup"><span data-stu-id="092c1-190">hello Get method response now includes hello new toodo item.</span></span>
15. <span data-ttu-id="092c1-191">Optioneel: Probeer ook Hallo Put, Delete, en Get by ID methoden.</span><span class="sxs-lookup"><span data-stu-id="092c1-191">Optional: Try also hello Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="092c1-192">Sluit Hallo browser en stop de foutopsporing van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="092c1-192">Close hello browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="092c1-193">Swashbuckle werkt met elk ASP.NET Web API-project.</span><span class="sxs-lookup"><span data-stu-id="092c1-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="092c1-194">Als u tooadd Swagger-metagegevens generatie tooan bestaand project wilt, gewoon Hallo Swashbuckle-pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="092c1-194">If you want tooadd Swagger metadata generation tooan existing project, just install hello Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="092c1-195">De Swagger-metagegevens bevatten voor elke API-bewerking een unieke id.</span><span class="sxs-lookup"><span data-stu-id="092c1-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="092c1-196">Standaard kan Swashbuckle dubbele Swagger-bewerkings-id's genereren voor uw Web API-controllermethoden.</span><span class="sxs-lookup"><span data-stu-id="092c1-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="092c1-197">Dit gebeurt als uw domeincontroller overbelaste HTTP-methoden bevat, zoals `Get()` en `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="092c1-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="092c1-198">Zie voor meer informatie over hoe toohandle overloads [aanpassen door Swashbuckle gegenereerde API-definities](app-service-api-dotnet-swashbuckle-customize.md).</span><span class="sxs-lookup"><span data-stu-id="092c1-198">For information about how toohandle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="092c1-199">Als u een Web API-project in Visual Studio met hello Azure API-App-sjabloon maakt, code die unieke bewerkings-id gegenereerd toohello wordt automatisch toegevoegd *SwaggerConfig.cs* bestand.</span><span class="sxs-lookup"><span data-stu-id="092c1-199">If you create a Web API project in Visual Studio by using hello Azure API App template, code that generates unique operation IDs is automatically added toohello *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="092c1-200"><a id="createapiapp"></a>Een API-app in Azure maken en implementeren van code tooit</span><span class="sxs-lookup"><span data-stu-id="092c1-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code tooit</span></span>
<span data-ttu-id="092c1-201">In deze sectie gebruikt u Azure-hulpprogramma's die zijn geïntegreerd met Visual Studio Hallo **webpublicatie** wizard toocreate een nieuwe API-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="092c1-201">In this section, you use Azure tools that are integrated into hello Visual Studio **Publish Web** wizard toocreate a new API app in Azure.</span></span> <span data-ttu-id="092c1-202">Vervolgens Hallo ToDoListDataAPI project toohello nieuwe API-app implementeren en Hallo API aanroepen door het uitvoeren van Hallo Swagger-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="092c1-202">Then you deploy hello ToDoListDataAPI project toohello new API app and call hello API by running hello Swagger UI.</span></span>

1. <span data-ttu-id="092c1-203">In **Solution Explorer**, met de rechtermuisknop op Hallo ToDoListDataAPI project en klik vervolgens op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="092c1-203">In **Solution Explorer**, right-click hello ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Klikken op Publish in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="092c1-205">In Hallo **profiel** stap Hallo **webpublicatie** wizard, klikt u op **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="092c1-205">In hello **Profile** step of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Klikken op Azure App Service in de wizard Publish Web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="092c1-207">Meld u aan tooyour Azure-account als u dit nog niet hebt gedaan of vernieuw uw referenties als deze zijn verlopen.</span><span class="sxs-lookup"><span data-stu-id="092c1-207">Sign in tooyour Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="092c1-208">In het dialoogvenster App Service Hallo, kiest u hello Azure **abonnement** u toouse wilt en klik vervolgens op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="092c1-208">In hello App Service dialog box, choose hello Azure **Subscription** you want toouse, and then click **New**.</span></span>
   
    ![Klikken op New in het dialoogvenster App Service](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="092c1-210">Hallo **Hosting** tabblad Hallo **Create App Service** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="092c1-210">hello **Hosting** tab of hello **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="092c1-211">Omdat u een Web-API-project dat swashbuckle is geïnstalleerd implementeert, Visual Studio wordt ervan uitgegaan dat u wilt dat toocreate een API-App.</span><span class="sxs-lookup"><span data-stu-id="092c1-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want toocreate an API App.</span></span> <span data-ttu-id="092c1-212">Dit wordt aangegeven door Hallo **API App Name** title en door Hallo feit die Hallo **wijzigingstype** vervolgkeuzelijst is ingesteld, te**API-App**.</span><span class="sxs-lookup"><span data-stu-id="092c1-212">This is indicated by hello **API App Name** title and by hello fact that hello **Change Type** drop-down list is set too**API App**.</span></span>
   
    ![App-type in het dialoogvenster App Service](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="092c1-214">Voer een **API App Name** die uniek is in Hallo *azurewebsites.net* domein.</span><span class="sxs-lookup"><span data-stu-id="092c1-214">Enter an **API App Name** that is unique in hello *azurewebsites.net* domain.</span></span> <span data-ttu-id="092c1-215">U kunt de standaardnaam Hallo die Visual Studio wordt voorgesteld accepteren.</span><span class="sxs-lookup"><span data-stu-id="092c1-215">You can accept hello default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="092c1-216">Als u een naam die iemand anders al gebruikt opgeeft, ziet u een rood uitroepteken toohello rechts.</span><span class="sxs-lookup"><span data-stu-id="092c1-216">If you enter a name that someone else has already used, you see a red exclamation mark toohello right.</span></span>
   
    <span data-ttu-id="092c1-217">Hallo URL van Hallo API-app worden `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="092c1-217">hello URL of hello API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="092c1-218">In Hallo **resourcegroep** omlaag, klikt u op **nieuw**, en voer vervolgens 'ToDoListGroup' of een andere naam desgewenst.</span><span class="sxs-lookup"><span data-stu-id="092c1-218">In hello **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="092c1-219">Een resourcegroep is een verzameling Azure-resources, zoals web-apps, databases, virtuele machines, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="092c1-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="092c1-220">Voor deze zelfstudie is het beste toocreate een nieuwe resourcegroep kunt dan eenvoudig toodelete in één stap die alle Azure-resources die u voor de zelfstudie Hallo maakt Hallo.</span><span class="sxs-lookup"><span data-stu-id="092c1-220">For this tutorial, it's best toocreate a new resource group because that makes it easy toodelete in one step all hello Azure resources that you create for hello tutorial.</span></span>
   
    <span data-ttu-id="092c1-221">In dit vak kunt u een bestaande [resourcegroep](../azure-resource-manager/resource-group-overview.md) selecteren of een nieuwe maken door een naam te typen die anders is dan alle bestaande resourcegroepen in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="092c1-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="092c1-222">Klik op Hallo **nieuw** knop volgende toohello **App Service-Plan** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="092c1-222">Click hello **New** button next toohello **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="092c1-223">Hallo Schermafbeelding toont voorbeeldwaarden voor **API App Name**, **abonnement**, en **resourcegroep** --de waarden zijn anders.</span><span class="sxs-lookup"><span data-stu-id="092c1-223">hello screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Het dialoogvenster App Service maken](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="092c1-225">In Hallo stappen maakt u een App Service-plan voor de nieuwe resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="092c1-225">In hello following steps you create an App Service plan for hello new resource group.</span></span> <span data-ttu-id="092c1-226">Een App Service-plan bevat Hallo rekenresources die door uw API-app wordt uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="092c1-226">An App Service plan specifies hello compute resources that your API app runs on.</span></span> <span data-ttu-id="092c1-227">Bijvoorbeeld, als u de gratis laag hello, uw API-app wordt uitgevoerd op gedeelde virtuele machines, terwijl voor sommige betaald lagen deze wordt uitgevoerd via exclusieve virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="092c1-227">For example, if you choose hello free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="092c1-228">Zie [Overzicht van App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) voor informatie over App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="092c1-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="092c1-229">In Hallo **Configure App Service Plan** dialoogvenster 'ToDoListPlan' of een andere naam invoeren als u liever.</span><span class="sxs-lookup"><span data-stu-id="092c1-229">In hello **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="092c1-230">In Hallo **locatie** vervolgkeuzelijst Kies Hallo locatie die het dichtst tooyou.</span><span class="sxs-lookup"><span data-stu-id="092c1-230">In hello **Location** drop-down list, choose hello location that is closest tooyou.</span></span>
   
    <span data-ttu-id="092c1-231">Met deze instelling bepaalt u in welk Azure-datacentrum uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="092c1-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="092c1-232">Kies een locatie sluiten tooyou toominimize [latentie](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span><span class="sxs-lookup"><span data-stu-id="092c1-232">Choose a location close tooyou toominimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="092c1-233">In Hallo **grootte** omlaag, klikt u op **vrije**.</span><span class="sxs-lookup"><span data-stu-id="092c1-233">In hello **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="092c1-234">Voor deze zelfstudie bieden Hallo gratis prijscategorie voldoende prestaties.</span><span class="sxs-lookup"><span data-stu-id="092c1-234">For this tutorial, hello free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="092c1-235">In Hallo **Configure App Service Plan** dialoogvenster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="092c1-235">In hello **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Klikken op OK in het dialoogvenster Configure App Service Plan](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="092c1-237">In Hallo **Create App Service** in het dialoogvenster, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="092c1-237">In hello **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Klikken op Create in het dialoogvenster Create App Service](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="092c1-239">Visual Studio maakt Hallo API-app en een publicatieprofiel met alle vereiste Hallo-instellingen voor Hallo API-app.</span><span class="sxs-lookup"><span data-stu-id="092c1-239">Visual Studio creates hello API app and a publish profile that has all of hello required settings for hello API app.</span></span> <span data-ttu-id="092c1-240">En vervolgens het openen van Hallo **webpublicatie** wizard, waar u toodeploy Hallo project.</span><span class="sxs-lookup"><span data-stu-id="092c1-240">Then it opens hello **Publish Web** wizard, which you'll use toodeploy hello project.</span></span>
    
    <span data-ttu-id="092c1-241">Hallo **webpublicatie** wizard wordt geopend op Hallo **verbinding** tabblad (Zie hieronder).</span><span class="sxs-lookup"><span data-stu-id="092c1-241">hello **Publish Web** wizard opens on hello **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="092c1-242">Op Hallo **verbinding** tabblad hello **Server** en **sitenaam** instellingen punt tooyour API-app.</span><span class="sxs-lookup"><span data-stu-id="092c1-242">On hello **Connection** tab, hello **Server** and **Site name** settings point tooyour API app.</span></span> <span data-ttu-id="092c1-243">Hallo **gebruikersnaam** en **wachtwoord** zijn implementatiereferenties die Azure voor u maakt.</span><span class="sxs-lookup"><span data-stu-id="092c1-243">hello **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="092c1-244">Na de implementatie opent Visual Studio een browser toohello **doel-URL** (oftewel Hallo enige doel van het **doel-URL**).</span><span class="sxs-lookup"><span data-stu-id="092c1-244">After deployment, Visual Studio opens a browser toohello **Destination URL** (that's hello only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="092c1-245">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="092c1-245">Click **Next**.</span></span>
    
    ![Klikken op Next op het tabblad Connection van de wizard Publish Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="092c1-247">Hallo volgende tabblad is Hallo **instellingen** tabblad (Zie hieronder).</span><span class="sxs-lookup"><span data-stu-id="092c1-247">hello next tab is hello **Settings** tab (shown below).</span></span> <span data-ttu-id="092c1-248">Hier kunt u wijzigen Hallo build configuration tabblad toodeploy een foutopsporingsversie voor [foutopsporing op afstand](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="092c1-248">Here you can change hello build configuration tab toodeploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="092c1-249">Hallo tabblad biedt ook diverse **opties voor het publiceren van bestand**:</span><span class="sxs-lookup"><span data-stu-id="092c1-249">hello tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="092c1-250">Aanvullende bestanden op de bestemming verwijderen</span><span class="sxs-lookup"><span data-stu-id="092c1-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="092c1-251">Voorcompileren tijdens het publiceren</span><span class="sxs-lookup"><span data-stu-id="092c1-251">Precompile during publishing</span></span>
    * <span data-ttu-id="092c1-252">Bestanden uitsluiten van de map App_Data Hallo</span><span class="sxs-lookup"><span data-stu-id="092c1-252">Exclude files from hello App_Data folder</span></span>
    
    <span data-ttu-id="092c1-253">Voor deze zelfstudie hebt u geen van deze opties nodig.</span><span class="sxs-lookup"><span data-stu-id="092c1-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="092c1-254">Zie [Procedure: een webproject implementeren met behulp van publicatie met één klik in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx) voor gedetailleerde uitleg over deze opties.</span><span class="sxs-lookup"><span data-stu-id="092c1-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="092c1-255">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="092c1-255">Click **Next**.</span></span>
    
    ![Klikken op Next op het tabblad Settings van de wizard Publish Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="092c1-257">Hierna volgt Hallo **Preview** tabblad (Zie hieronder), waarmee u een kans toosee welke bestanden toobe gekopieerd van uw project toohello API-app gaat.</span><span class="sxs-lookup"><span data-stu-id="092c1-257">Next is hello **Preview** tab (shown below), which gives you an opportunity toosee what files are going toobe copied from your project toohello API app.</span></span> <span data-ttu-id="092c1-258">Wanneer u een project tooan API-app die u hebt al geïmplementeerd tooearlier implementeert, worden alleen de gewijzigde bestanden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="092c1-258">When you're deploying a project tooan API app that you already deployed tooearlier, only changed files are copied.</span></span> <span data-ttu-id="092c1-259">Als u een lijst met wat er wordt gekopieerd toosee wilt, kunt u Hallo **Start Preview** knop.</span><span class="sxs-lookup"><span data-stu-id="092c1-259">If you want toosee a list of what will be copied, you can click hello **Start Preview** button.</span></span>
15. <span data-ttu-id="092c1-260">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="092c1-260">Click **Publish**.</span></span>
    
    ![Klikken op Publish op het tabblad Preview van de wizard Publish Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="092c1-262">Visual Studio implementeert Hallo ToDoListDataAPI project toohello nieuwe API-app.</span><span class="sxs-lookup"><span data-stu-id="092c1-262">Visual Studio deploys hello ToDoListDataAPI project toohello new API app.</span></span> <span data-ttu-id="092c1-263">Hallo **uitvoer** venster Logboeken geslaagde implementatie en een 'is gemaakt' pagina wordt weergegeven in een browser geopend venster toohello URL van Hallo API-app.</span><span class="sxs-lookup"><span data-stu-id="092c1-263">hello **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened toohello URL of hello API app.</span></span>
    
    ![Bevestiging van geslaagde implementatie in het venster Output](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Pagina met melding dat de nieuwe API-app is gemaakt](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="092c1-266">'Swagger' toohello URL toevoegen in de adresbalk van Hallo browser en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="092c1-266">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="092c1-267">(Hallo-URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="092c1-267">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="092c1-268">Hallo browser geeft dezelfde Swagger-gebruikersinterface die u eerder hebt gezien, maar nu wordt uitgevoerd in de cloud Hallo Hallo weer.</span><span class="sxs-lookup"><span data-stu-id="092c1-268">hello browser displays hello same Swagger UI that you saw earlier, but now it's running in hello cloud.</span></span> <span data-ttu-id="092c1-269">Probeer Hallo Get-methode en u ziet dat je back toohello standaard 2 taakitems.</span><span class="sxs-lookup"><span data-stu-id="092c1-269">Try out hello Get method, and you see that you're back toohello default 2 to-do items.</span></span> <span data-ttu-id="092c1-270">Hallo-wijzigingen die u eerder hebt gemaakt zijn opgeslagen in het geheugen van de lokale computer Hallo.</span><span class="sxs-lookup"><span data-stu-id="092c1-270">hello changes you made earlier were saved in memory in hello local machine.</span></span>
17. <span data-ttu-id="092c1-271">Open Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="092c1-271">Open hello [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="092c1-272">Hello Azure-portal is een webinterface voor het beheer van Azure-bronnen zoals API-apps.</span><span class="sxs-lookup"><span data-stu-id="092c1-272">hello Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="092c1-273">Klik op **Meer Services > App Services**.</span><span class="sxs-lookup"><span data-stu-id="092c1-273">Click **More Services > App Services**.</span></span>
    
    ![Bladeren door App Services](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="092c1-275">In Hallo **App Services** blade zoeken en klikt u op uw nieuwe API-app.</span><span class="sxs-lookup"><span data-stu-id="092c1-275">In hello **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="092c1-276">(In hello Azure-portal, windows dat toohello rechts openen genoemd *blades*.)</span><span class="sxs-lookup"><span data-stu-id="092c1-276">(In hello Azure portal, windows that open toohello right are called *blades*.)</span></span>
    
    ![De blade App Services](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="092c1-278">Er worden twee blades geopend.</span><span class="sxs-lookup"><span data-stu-id="092c1-278">Two blades open.</span></span> <span data-ttu-id="092c1-279">Een blade bevat een overzicht van Hallo API-app en een heeft een lange lijst met instellingen die u kunt weergeven en wijzigen.</span><span class="sxs-lookup"><span data-stu-id="092c1-279">One blade has an overview of hello API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="092c1-280">In Hallo **instellingen** blade, zoeken Hallo **API** sectie en klik op **API-definitie**.</span><span class="sxs-lookup"><span data-stu-id="092c1-280">In hello **Settings** blade, find hello **API** section and click **API Definition**.</span></span>
    
    ![API-definitie op de blade Instellingen](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="092c1-282">Hallo **API-definitie** blade kunt u opgeven Hallo-URL die de metagegevens van Swagger 2.0 JSON-indeling retourneert.</span><span class="sxs-lookup"><span data-stu-id="092c1-282">hello **API Definition** blade lets you specify hello URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="092c1-283">Als u Visual Studio Hallo API-app maakt, wordt Hallo API-definitie URL toohello-standaardwaarde voor door Swashbuckle gegenereerde metagegevens die u eerder hebt gezien dat Hallo API-app van de basis URL plus `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="092c1-283">When Visual Studio creates hello API app, it sets hello API definition URL toohello default value for Swashbuckle-generated metadata that you saw earlier, which is hello API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![URL van de API-definitie](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="092c1-285">Wanneer u een API-app toogenerate client-code voor deze selecteert, haalt Visual Studio Hallo metagegevens van deze URL.</span><span class="sxs-lookup"><span data-stu-id="092c1-285">When you select an API app toogenerate client code for it, Visual Studio retrieves hello metadata from this URL.</span></span>

## <span data-ttu-id="092c1-286"><a id="codegen"></a>Genereren van clientcode voor Hallo gegevenslaag</span><span class="sxs-lookup"><span data-stu-id="092c1-286"><a id="codegen"></a> Generate client code for hello data tier</span></span>
<span data-ttu-id="092c1-287">Een van de voordelen van de integratie van Swagger in Azure API-apps Hallo is automatisch genereren van code.</span><span class="sxs-lookup"><span data-stu-id="092c1-287">One of hello advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="092c1-288">Gegenereerde clientklassen maken het gemakkelijker toowrite-code die een API-app aanroept.</span><span class="sxs-lookup"><span data-stu-id="092c1-288">Generated client classes make it easier toowrite code that calls an API app.</span></span>

<span data-ttu-id="092c1-289">Hallo ToDoListAPI-project bevat al de clientcode Hallo gegenereerd, maar in de volgende stappen uit Hallo past u deze verwijderen en opnieuw genereren toosee hoe toodo Hallo genereren van code.</span><span class="sxs-lookup"><span data-stu-id="092c1-289">hello ToDoListAPI project already has hello generated client code, but in hello following steps you'll delete it and regenerate it toosee how toodo hello code generation.</span></span>

1. <span data-ttu-id="092c1-290">In Visual Studio **Solution Explorer**in Hallo ToDoListAPI-project, Hallo verwijderen, *ToDoListDataAPI* map.</span><span class="sxs-lookup"><span data-stu-id="092c1-290">In Visual Studio **Solution Explorer**, in hello ToDoListAPI project, delete hello *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="092c1-291">**Waarschuwing: Alleen Hallo map, niet Hallo-project ToDoListDataAPI verwijderen.**</span><span class="sxs-lookup"><span data-stu-id="092c1-291">**Caution: Delete only hello folder, not hello ToDoListDataAPI project.**</span></span>
   
    ![Gegenereerde clientcode verwijderen](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="092c1-293">Deze map is gemaakt met behulp van Hallo codeproces voor het genereren waarmee u over toogo via bent.</span><span class="sxs-lookup"><span data-stu-id="092c1-293">This folder was created by using hello code generation process that you're about toogo through.</span></span>
2. <span data-ttu-id="092c1-294">Met de rechtermuisknop op Hallo ToDoListAPI-project en klik vervolgens op **Add > REST API Client**.</span><span class="sxs-lookup"><span data-stu-id="092c1-294">Right-click hello ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![REST-API-client toevoegen in Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="092c1-296">In Hallo **Add REST API Client** in het dialoogvenster, klikt u op **Swagger URL**, en klik vervolgens op **Select Azure Asset**.</span><span class="sxs-lookup"><span data-stu-id="092c1-296">In hello **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Azure-asset selecteren](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="092c1-298">In Hallo **App Service** in het dialoogvenster vouwt u Hallo-resourcegroep die u voor deze zelfstudie en selecteer uw API-app en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="092c1-298">In hello **App Service** dialog box, expand hello resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![API-app selecteren voor het genereren van code](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="092c1-300">Merk op dat wanneer u toohello terugkeert **Add REST API Client** dialoogvenster Hallo tekstvak is ingevuld Hallo API-definitie URL-waarde die u eerder in de portal Hallo hebt gezien.</span><span class="sxs-lookup"><span data-stu-id="092c1-300">Notice that when you return toohello **Add REST API Client** dialog, hello text box has been filled in with hello API definition URL value that you saw earlier in hello portal.</span></span>
   
    ![URL van de API-definitie](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="092c1-302">Een andere manier tooget-metagegevens voor het genereren van code is tooenter Hallo URL rechtstreeks in plaats van het Hallo-bladervenster doorlopen.</span><span class="sxs-lookup"><span data-stu-id="092c1-302">An alternative way tooget metadata for code generation is tooenter hello URL directly instead of going through hello browse dialog.</span></span> <span data-ttu-id="092c1-303">Of als u clientcode toogenerate wilt voordat u tooAzure implementeert, kan Hallo Web API-project lokaal uitvoeren, Ga toohello URL waarmee Hallo Swagger JSON-bestand, Hallo-bestand opslaan en hello gebruiken **Selecteer een bestaand bestand Swagger-metagegevens**optie.</span><span class="sxs-lookup"><span data-stu-id="092c1-303">Or if you want toogenerate client code before deploying tooAzure, you could run hello Web API project locally, go toohello URL that provides hello Swagger JSON file, save hello file, and use hello **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="092c1-304">In Hallo **Add REST API Client** in het dialoogvenster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="092c1-304">In hello **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="092c1-305">Visual Studio maakt een map met de naam van Hallo API-app en genereert clientklassen.</span><span class="sxs-lookup"><span data-stu-id="092c1-305">Visual Studio creates a folder named after hello API app and generates client classes.</span></span>
   
    ![Codebestanden voor gegenereerde client](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="092c1-307">Open in het project ToDoListAPI hello *Controllers\ToDoListController.cs* toosee Hallo code op de regel 40 die Hallo-API aanroept met behulp van de client Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="092c1-307">In hello ToDoListAPI project, open *Controllers\ToDoListController.cs* toosee hello code at line 40  that calls hello API by using hello generated client.</span></span>
   
    <span data-ttu-id="092c1-308">Hallo volgende fragment toont hoe Hallo code Hallo clientobject instantieert en aanroepen Hallo Get-methode.</span><span class="sxs-lookup"><span data-stu-id="092c1-308">hello following snippet shows how hello code instantiates hello client object and calls hello Get method.</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));
            return client;
        }
   
        public async Task<IEnumerable<ToDoItem>> Get()
        {
            using (var client = NewDataAPIClient())
            {
                var results = await client.ToDoList.GetByOwnerAsync(owner);
                return results.Select(m => new ToDoItem
                {
                    Description = m.Description,
                    ID = (int)m.ID,
                    Owner = m.Owner
                });
            }
        }
   
    <span data-ttu-id="092c1-309">Hallo-constructorparameter haalt Hallo eindpunt-URL van Hallo `toDoListDataAPIURL` app-instelling.</span><span class="sxs-lookup"><span data-stu-id="092c1-309">hello constructor parameter gets hello endpoint URL from  hello `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="092c1-310">In Hallo Web.config-bestand wordt die waarde set toohello lokale IIS Express URL Hallo API project, zodat u de toepassing hello lokaal kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="092c1-310">In hello Web.config file, that value is set toohello local IIS Express URL of hello API project so that you can run hello application locally.</span></span> <span data-ttu-id="092c1-311">Als u Hallo constructorparameter weglaat, is het standaardeindpunt Hallo Hallo-URL die u hebt gegenereerd Hallo code uit.</span><span class="sxs-lookup"><span data-stu-id="092c1-311">If you omit hello constructor parameter, hello default endpoint is hello URL that you generated hello code from.</span></span>
7. <span data-ttu-id="092c1-312">De clientklasse wordt gegenereerd met een andere naam op basis van de naam van uw API-app; Hallo-code in wijzigen *Controllers\ToDoListController.cs* zodat hello typenaam overeenkomt met wat in uw project is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="092c1-312">Your client class will be generated with a different name based on your API app name; change hello code in *Controllers\ToDoListController.cs* so that hello type name matches what was generated in your project.</span></span> <span data-ttu-id="092c1-313">Als de naam van uw API-app bijvoorbeeld ToDoListDataAPI071316 is, zou u deze code wijzigen:</span><span class="sxs-lookup"><span data-stu-id="092c1-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="092c1-314">toothis:</span><span class="sxs-lookup"><span data-stu-id="092c1-314">toothis:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-toohost-hello-middle-tier"></a><span data-ttu-id="092c1-315">Een API-app toohost Hallo middelste laag maken</span><span class="sxs-lookup"><span data-stu-id="092c1-315">Create an API app toohost hello middle tier</span></span>
<span data-ttu-id="092c1-316">Eerder u [Hallo gegevens laag API-app gemaakt en geïmplementeerd code tooit](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="092c1-316">Earlier you [created hello data tier API app and deployed code tooit](#createapiapp).</span></span>  <span data-ttu-id="092c1-317">Nu u Hallo Volg dezelfde procedure voor de middelste laag API-app Hallo.</span><span class="sxs-lookup"><span data-stu-id="092c1-317">Now you follow hello same procedure for hello middle tier API app.</span></span>

1. <span data-ttu-id="092c1-318">In **Solution Explorer**, klik met de rechtermuisknop Hallo middelste laag ToDoListAPI-project (geen Hallo gegevenslaag ToDoListDataAPI) en klik vervolgens op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="092c1-318">In **Solution Explorer**, right-click hello middle tier ToDoListAPI  project (not hello data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Klikken op Publish in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="092c1-320">In Hallo **profiel** tabblad Hallo **webpublicatie** wizard, klikt u op **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="092c1-320">In hello **Profile** tab of hello **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="092c1-321">In Hallo **App Service** in het dialoogvenster, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="092c1-321">In hello **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="092c1-322">In Hallo **Hosting** tabblad Hallo **Create App Service** dialoogvenster vak, accepteer de standaardinstelling Hallo **API App Name** of geef een naam die uniek is in Hallo  *azurewebsites.NET* domein.</span><span class="sxs-lookup"><span data-stu-id="092c1-322">In hello **Hosting** tab of hello **Create App Service** dialog box, accept hello default **API App Name** or enter a name that is unique in hello *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="092c1-323">Kies hello Azure **abonnement** u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="092c1-323">Choose hello Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="092c1-324">In Hallo **resourcegroep** vervolgkeuzelijst, kiest u Hallo dezelfde resourcegroep die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="092c1-324">In hello **Resource Group** drop-down, choose hello same resource group you created earlier.</span></span>
7. <span data-ttu-id="092c1-325">In Hallo **App Service-abonnement** vervolgkeuzelijst, kiest u Hallo hetzelfde abonnement dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="092c1-325">In hello **App Service Plan** drop-down, choose hello same plan you created earlier.</span></span> <span data-ttu-id="092c1-326">Wordt standaard toothat waarde.</span><span class="sxs-lookup"><span data-stu-id="092c1-326">It will default toothat value.</span></span>
8. <span data-ttu-id="092c1-327">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="092c1-327">Click **Create**.</span></span>
   
    <span data-ttu-id="092c1-328">Visual Studio maakt Hallo API-app, maakt er een publicatieprofiel voor en geeft weer Hallo **verbinding** stap Hallo **webpublicatie** wizard.</span><span class="sxs-lookup"><span data-stu-id="092c1-328">Visual Studio creates hello API app, creates a publish profile for it, and displays hello **Connection** step of hello **Publish Web** wizard.</span></span>
9. <span data-ttu-id="092c1-329">In Hallo **verbinding** stap Hallo **webpublicatie** wizard, klikt u op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="092c1-329">In hello **Connection** step of hello **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="092c1-330">Visual Studio Hallo ToDoListAPI-project toohello nieuwe API-app implementeert en een URL van de browser toohello van Hallo API-app wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="092c1-330">Visual Studio deploys hello ToDoListAPI project toohello new API app and opens a browser toohello URL of hello API app.</span></span> <span data-ttu-id="092c1-331">Hallo 'is gemaakt' pagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="092c1-331">hello "successfully created" page appears.</span></span>

## <a name="configure-hello-middle-tier-toocall-hello-data-tier"></a><span data-ttu-id="092c1-332">Hallo middelste laag toocall Hallo-gegevenslaag configureren</span><span class="sxs-lookup"><span data-stu-id="092c1-332">Configure hello middle tier toocall hello data tier</span></span>
<span data-ttu-id="092c1-333">Als u de API-app voor Hallo middelste laag nu aangeroepen, probeert deze toocall Hallo-gegevenslaag met Hallo localhost-URL die wordt nog steeds Hallo Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="092c1-333">If you called hello middle tier API app now, it would try toocall hello data tier using hello localhost URL that is still in hello Web.config file.</span></span> <span data-ttu-id="092c1-334">In deze sectie voert u Hallo gegevens laag API-app-URL in een omgevingsinstelling in Hallo middelste laag API-app.</span><span class="sxs-lookup"><span data-stu-id="092c1-334">In this section you enter hello data tier API app URL into an environment setting in hello middle tier API app.</span></span> <span data-ttu-id="092c1-335">Wanneer hello code in de middelste laag API-app Hallo Hallo gegevens laag URL-instelling ophaalt, overschrijft Hallo omgevingsinstelling wat is er in Hallo Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="092c1-335">When hello code in hello middle tier API app retrieves hello data tier URL setting, hello environment setting will override what's in hello Web.config file.</span></span>

1. <span data-ttu-id="092c1-336">Ga toohello [Azure-portal](https://portal.azure.com/), en navigeert u vervolgens toohello **API-App** blade voor Hallo API-app die u hebt gemaakt project toohost Hallo-TodoListAPI (middelste laag).</span><span class="sxs-lookup"><span data-stu-id="092c1-336">Go toohello [Azure portal](https://portal.azure.com/), and then navigate toohello **API App** blade for hello API app that you created toohost hello TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="092c1-337">Hallo in API-App **instellingen** blade, klikt u op **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="092c1-337">In hello API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="092c1-338">Hallo in API-App **toepassingsinstellingen** blade, schuif omlaag toohello **appinstellingen** sectie en voeg de volgende Hallo sleutel en waarde.</span><span class="sxs-lookup"><span data-stu-id="092c1-338">In hello API App's **Application Settings** blade, scroll down toohello **App settings** section and add hello following key and value.</span></span> <span data-ttu-id="092c1-339">Hallo-waarde is Hallo-URL van Hallo eerste API-App die u in deze zelfstudie hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="092c1-339">hello value will be hello URL of hello first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="092c1-340">**Sleutel**</span><span class="sxs-lookup"><span data-stu-id="092c1-340">**Key**</span></span> | <span data-ttu-id="092c1-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="092c1-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="092c1-342">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="092c1-342">**Value**</span></span> |<span data-ttu-id="092c1-343">https://{de naam van uw API-app voor de gegevenslaag}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="092c1-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="092c1-344">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="092c1-344">**Example**</span></span> |<span data-ttu-id="092c1-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="092c1-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="092c1-346">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="092c1-346">Click **Save**.</span></span>
   
    ![Klikken op Opslaan in het gedeelte App-instellingen](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="092c1-348">Wanneer het Hallo-code wordt uitgevoerd in Azure, overschrijft deze waarde Hallo localhost-URL die zich in Hallo Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="092c1-348">When hello code runs in Azure, this value will now override hello localhost URL that is in hello Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="092c1-349">Test</span><span class="sxs-lookup"><span data-stu-id="092c1-349">Test</span></span>
1. <span data-ttu-id="092c1-350">Blader in een browservenster toohello-URL van Hallo nieuwe middelste laag API-app die u zojuist hebt gemaakt voor ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="092c1-350">In a browser window, browse toohello URL of hello new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="092c1-351">U kunt er ophalen door te klikken op Hallo-URL in de hoofdblade Hallo API-app in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="092c1-351">You can get there by clicking hello URL in hello API app's main blade in hello portal.</span></span>
2. <span data-ttu-id="092c1-352">'Swagger' toohello URL toevoegen in de adresbalk van Hallo browser en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="092c1-352">Add "swagger" toohello URL in hello browser's address bar, and then press Enter.</span></span> <span data-ttu-id="092c1-353">(Hallo-URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="092c1-353">(hello URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="092c1-354">Hallo browser geeft Hallo dezelfde Swagger-gebruikersinterface die u eerder hebt gezien voor ToDoListDataAPI, maar nu `owner` is niet een verplicht veld voor Hallo Get-bewerking, omdat Hallo middelste laag API-app voor u die waarde toohello API app voor de gegevenslaag verzendt.</span><span class="sxs-lookup"><span data-stu-id="092c1-354">hello browser displays hello same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for hello Get operation, because hello middle tier API app is sending that value toohello data tier API app for you.</span></span> <span data-ttu-id="092c1-355">(Als u zelfstudies over verificatie volgt hello, stuurt Hallo middelste laag werkelijke gebruikers-id's voor Hallo `owner` parameter; voor nu er wordt hard-coding van een sterretje.)</span><span class="sxs-lookup"><span data-stu-id="092c1-355">(When you do hello authentication tutorials, hello middle tier will send actual user IDs for hello `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="092c1-356">Probeer Hallo Get-methode en hello andere methoden toovalidate die Hallo middelste laag API-app op correcte wijze aanroept Hallo gegevenslaag API-app.</span><span class="sxs-lookup"><span data-stu-id="092c1-356">Try out hello Get method and hello other methods toovalidate that hello middle tier API app is successfully calling hello data tier API app.</span></span>
   
    ![Get-methode van de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="092c1-358">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="092c1-358">Troubleshooting</span></span>
<span data-ttu-id="092c1-359">Als u tijdens het doorlopen van deze zelfstudie tegen problemen aanloopt, vindt u hier enkele ideeën voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="092c1-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="092c1-360">Zorg ervoor dat u de meest recente versie Hallo Hallo [Azure SDK voor .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="092c1-360">Make sure that you're using hello latest version of hello [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="092c1-361">Twee van de projectnamen Hallo zijn elkaar (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="092c1-361">Two of hello project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="092c1-362">Als dingen niet zo uitzien zoals beschreven in Hallo instructies wanneer u met een project werkt, zorg er dan voor dat u de juiste Hallo-project hebt geopend.</span><span class="sxs-lookup"><span data-stu-id="092c1-362">If things don't look as described in hello instructions when you are working with a project, make sure you have opened hello correct project.</span></span>
* <span data-ttu-id="092c1-363">Als u een bedrijfsnetwerk en toodeploy tooAzure App Service via een firewall probeert, zorg ervoor dat de poorten 443 en 8172 geopend voor Web Deploy zijn.</span><span class="sxs-lookup"><span data-stu-id="092c1-363">If you're on a corporate network and are trying toodeploy tooAzure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="092c1-364">Als u deze poorten niet kunt openen, gebruik dan een andere implementatiemethode.</span><span class="sxs-lookup"><span data-stu-id="092c1-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="092c1-365">Zie [implementeren van uw app tooAzure App Service](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="092c1-365">See [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="092c1-366">Fouten 'routenamen moeten uniek zijn'--mogelijk doen deze als u per ongeluk Hallo verkeerde project tooan API-app implementeren en vervolgens de juiste één tooit Hallo later implementeren.</span><span class="sxs-lookup"><span data-stu-id="092c1-366">"Route names must be unique" errors -- you could get these if you accidentally deploy hello wrong project tooan API app and then later deploy hello correct one tooit.</span></span> <span data-ttu-id="092c1-367">toocorrect deze, de implementatie opnieuw Hallo juiste project toohello API-app en op Hallo **instellingen** tabblad Hallo **webpublicatie** wizard selecteert **verwijderen van aanvullende bestanden op de bestemming**.</span><span class="sxs-lookup"><span data-stu-id="092c1-367">toocorrect this, redeploy hello correct project toohello API app, and on hello **Settings** tab of hello **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="092c1-368">Nadat u uw ASP.NET-API-app uitgevoerd in Azure App Service hebt, kunt u toolearn meer over de functies van Visual Studio die probleemoplossing vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="092c1-368">After you have your ASP.NET API app running in Azure App Service, you may want toolearn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="092c1-369">Voor meer informatie over logboekregistratie, foutopsporing op afstand en meer raadpleegt u [Problemen met Azure App Service-apps in Visual Studio oplossen](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="092c1-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="092c1-370">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="092c1-370">Next steps</span></span>
<span data-ttu-id="092c1-371">U hebt gezien hoe toodeploy bestaande Web-API-projecten tooAPI apps genereren van clientcode voor API-apps en API-apps vanuit .NET-clients gebruiken.</span><span class="sxs-lookup"><span data-stu-id="092c1-371">You've seen how toodeploy existing Web API projects tooAPI apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="092c1-372">Hallo volgende zelfstudie in deze reeks ziet u hoe te[CORS tooconsume API apps vanuit JavaScript-clients gebruiken](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="092c1-372">hello next tutorial in this series shows how too[use CORS tooconsume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="092c1-373">Zie voor meer informatie over client-codegeneratie Hallo [Azure/AutoRest](https://github.com/azure/autorest) opslagplaats op GitHub.com. Voor hulp bij problemen met behulp van de client gegenereerd hello, opent u een [probleem in de AutoRest-opslagplaats Hallo](https://github.com/azure/autorest/issues).</span><span class="sxs-lookup"><span data-stu-id="092c1-373">For more information about client code generation, see hello [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com. For help with problems using hello generated client, open an [issue in hello AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="092c1-374">Als u toocreate nieuwe API-app-projecten maken wilt, gebruikt u Hallo **Azure API-App** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="092c1-374">If you want toocreate new API app projects from scratch, use hello **Azure API App** template.</span></span>

![API-app-sjabloon in Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="092c1-376">Hallo **Azure API-App** projectsjabloon is gelijkwaardig toochoosing hello **leeg** ASP.NET 4.5.2-sjabloon sjabloon, te klikken op Hallo selectievakje tooadd Web API-ondersteuning en Hallo Swashbuckle NuGet-pakket installeert.</span><span class="sxs-lookup"><span data-stu-id="092c1-376">hello **Azure API App** project template is equivalent toochoosing hello **Empty** ASP.NET 4.5.2 template, clicking hello check box tooadd Web API support, and installing hello Swashbuckle NuGet package.</span></span> <span data-ttu-id="092c1-377">Hallo-sjabloon wordt bovendien sommige Swashbuckle configuratie code ontworpen tooprevent Hallo maken van dubbele Swagger-bewerkings-id's toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="092c1-377">In addition, hello template adds some Swashbuckle configuration code designed tooprevent hello creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="092c1-378">Als u een API-App-project hebt gemaakt, kunt u dit implementeren tooan API app Hallo dezelfde manier als u in deze zelfstudie hebt gezien.</span><span class="sxs-lookup"><span data-stu-id="092c1-378">Once you've created an API App project, you can deploy it tooan API app hello same way you saw in this tutorial.</span></span>


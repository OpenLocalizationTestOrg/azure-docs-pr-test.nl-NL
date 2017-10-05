---
title: Aan de slag met API Apps en ASP.NET in App Service | Microsoft Docs
description: Ontdek hoe u met behulp van Visual Studio 2015 een ASP.NET API-app maakt, implementeert en gebruikt in Azure App Service.
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
ms.openlocfilehash: e8fbffde29efcdbb2f67362474061e9f6ee0d59d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-api-apps-aspnet-and-swagger-in-azure-app-service"></a><span data-ttu-id="efe9a-103">Aan de slag met API-apps, ASP.NET en Swagger in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="efe9a-103">Get started with API Apps, ASP.NET, and Swagger in Azure App Service</span></span>
[!INCLUDE [selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="efe9a-104">Dit is de eerste van een reeks zelfstudies die laten zien hoe u functies van Azure App Service kunt gebruiken die handig zijn voor het ontwikkelen en hosten van RESTful-API's.</span><span class="sxs-lookup"><span data-stu-id="efe9a-104">This is the first in a series of tutorials that show how to use features of Azure App Service that are helpful for developing and hosting RESTful APIs.</span></span>  <span data-ttu-id="efe9a-105">In deze zelfstudie wordt ondersteuning voor API-metagegevens in Swagger-indeling besproken.</span><span class="sxs-lookup"><span data-stu-id="efe9a-105">This tutorial covers support for API metadata in Swagger format.</span></span>

<span data-ttu-id="efe9a-106">U leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="efe9a-106">You'll learn:</span></span>

* <span data-ttu-id="efe9a-107">Het maken en implementeren van [API-apps](app-service-api-apps-why-best-platform.md) in Azure App Service met behulp van hulpprogramma's die zijn ingebouwd in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="efe9a-107">How to create and deploy [API apps](app-service-api-apps-why-best-platform.md) in Azure App Service by using tools built into Visual Studio 2015.</span></span>
* <span data-ttu-id="efe9a-108">Het automatiseren van API-detectie met behulp van het Swashbuckle NuGet-pakket om Swagger API-metagegevens dynamisch te genereren.</span><span class="sxs-lookup"><span data-stu-id="efe9a-108">How to automate API discovery by using the Swashbuckle NuGet package to dynamically generate Swagger API metadata.</span></span>
* <span data-ttu-id="efe9a-109">Het gebruik van Swagger API-metagegevens voor het automatisch genereren van clientcode voor een API-app.</span><span class="sxs-lookup"><span data-stu-id="efe9a-109">How to use Swagger API metadata to automatically generate client code for an API app.</span></span>

## <a name="sample-application-overview"></a><span data-ttu-id="efe9a-110">Overzicht van voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="efe9a-110">Sample application overview</span></span>
<span data-ttu-id="efe9a-111">In deze zelfstudie werkt u met een voorbeeld van een eenvoudige takenlijsttoepassing.</span><span class="sxs-lookup"><span data-stu-id="efe9a-111">In this tutorial, you work with a simple to-do list sample application.</span></span> <span data-ttu-id="efe9a-112">De toepassing heeft een SPA-front-end (SPA staat voor 'Single-Page Application'), een ASP.NET-web-API als middelste laag en een ASP.NET-web-API als gegevenslaag.</span><span class="sxs-lookup"><span data-stu-id="efe9a-112">The application has a single-page application (SPA) front end, an ASP.NET Web API middle tier, and an ASP.NET Web API data tier.</span></span>

![Diagram van API-apps-voorbeeldtoepassing](./media/app-service-api-dotnet-get-started/noauthdiagram.png)

<span data-ttu-id="efe9a-114">Hier volgt een schermafbeelding van de [AngularJS](https://angularjs.org/)-front-end.</span><span class="sxs-lookup"><span data-stu-id="efe9a-114">Here's a screen shot of the [AngularJS](https://angularjs.org/) front end.</span></span>

![Voorbeeld van API-apps-takenlijsttoepassing](./media/app-service-api-dotnet-get-started/todospa.png)

<span data-ttu-id="efe9a-116">De Visual Studio-oplossing omvat drie projecten:</span><span class="sxs-lookup"><span data-stu-id="efe9a-116">The Visual Studio solution includes three projects:</span></span>

![](./media/app-service-api-dotnet-get-started/projectsinse.png)

* <span data-ttu-id="efe9a-117">**ToDoListAngular** - de front end: een AngularJS SPA die de middelste laag aanroept.</span><span class="sxs-lookup"><span data-stu-id="efe9a-117">**ToDoListAngular** - The front end: an AngularJS SPA that calls the middle tier.</span></span>
* <span data-ttu-id="efe9a-118">**ToDoListAPI** - de middelste laag: een ASP.NET Web API-project dat de gegevenslaag aanroept om CRUD-bewerkingen uit te voeren op taken.</span><span class="sxs-lookup"><span data-stu-id="efe9a-118">**ToDoListAPI** - The middle tier: an ASP.NET Web API project that calls the data tier to perform CRUD operations on to-do items.</span></span>
* <span data-ttu-id="efe9a-119">**ToDoListAPI** - de gegevenslaag: een ASP.NET Web API-project dat CRUD-bewerkingen uitvoert op taken.</span><span class="sxs-lookup"><span data-stu-id="efe9a-119">**ToDoListDataAPI** - The data tier:  an ASP.NET Web API project that performs CRUD operations on to-do items.</span></span>

<span data-ttu-id="efe9a-120">De architectuur met drie lagen is een van de vele architecturen die u kunt implementeren met behulp van API-apps en wordt hier alleen voor demonstratiedoeleinden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-120">The three-tier architecture is one of many architectures that you can implement by using API Apps and is used here only for demonstration purposes.</span></span> <span data-ttu-id="efe9a-121">Ter illustratie van de functies van API-apps is de code in elke laag zo eenvoudig mogelijk gehouden. De gegevenslaag maakt bijvoorbeeld voor persistentie gebruik van het geheugen van de server in plaats van een database.</span><span class="sxs-lookup"><span data-stu-id="efe9a-121">The code in each tier is as simple as possible to demonstrate API Apps features; for example, the data tier uses server memory rather than a database as its persistence mechanism.</span></span>

<span data-ttu-id="efe9a-122">Nadat u deze zelfstudie hebt voltooid, beschikt u over twee Web API-projecten die in de cloud worden uitgevoerd in App Service API-apps.</span><span class="sxs-lookup"><span data-stu-id="efe9a-122">On completing this tutorial, you'll have the two Web API projects up and running in the cloud in App Service API apps.</span></span>

<span data-ttu-id="efe9a-123">In de volgende zelfstudie in de reeks wordt de SPA-front-end in de cloud geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-123">The next tutorial in the series deploys the SPA front end to the cloud.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efe9a-124">Vereisten</span><span class="sxs-lookup"><span data-stu-id="efe9a-124">Prerequisites</span></span>
* <span data-ttu-id="efe9a-125">ASP.NET Web API: in de instructies in de zelfstudie wordt ervan uitgegaan dat u beschikt over basiskennis van het werken met ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="efe9a-125">ASP.NET Web API - The tutorial instructions assume you have a basic knowledge of how to work with ASP.NET [Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) in Visual Studio.</span></span>
* <span data-ttu-id="efe9a-126">Azure-account: u kunt [een gratis Azure-account openen](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="efe9a-126">Azure account - You can [Open an Azure account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) or [Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
  
    <span data-ttu-id="efe9a-127">Als u met Azure App Service aan de slag wilt voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="efe9a-127">If you want to get started with Azure App Service before you sign up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/).</span></span> <span data-ttu-id="efe9a-128">Daar kunt u direct een eenvoudige, tijdelijke app maken in App Service. U hebt hiervoor **geen creditcard nodig** en bent nergens toe verplicht.</span><span class="sxs-lookup"><span data-stu-id="efe9a-128">There, you can immediately create a short-lived starter app in App Service — **no credit card required**, and no commitments.</span></span>
* <span data-ttu-id="efe9a-129">Visual Studio 2015 met de [Azure SDK voor .NET](https://azure.microsoft.com/downloads/archive-net-downloads/): de SDK installeert automatisch Visual Studio 2015 als u dit nog niet hebt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-129">Visual Studio 2015 with the [Azure SDK for .NET](https://azure.microsoft.com/downloads/archive-net-downloads/) - The SDK installs Visual Studio 2015 automatically if you don't already have it.</span></span>
  
  * <span data-ttu-id="efe9a-130">Klik in Visual Studio op Help -> Over Microsoft Visual Studio en zorg ervoor dat 'Azure App Service Tools v2.9.1' of hoger is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-130">In Visual Studio, click Help -> About Microsoft Visual Studio and ensure that you have "Azure App Service Tools v2.9.1" or higher installed.</span></span>
    
    ![Versie van Azure App Tools](./media/app-service-api-dotnet-get-started/apiversion.png)
    
    > [!NOTE]
    > <span data-ttu-id="efe9a-132">Afhankelijk van hoeveel van de SDK-afhankelijkheden u al op uw computer hebt staan, kan het installeren van de SDK lang duren, van enkele minuten tot een halfuur of meer.</span><span class="sxs-lookup"><span data-stu-id="efe9a-132">Depending on how many of the SDK dependencies you already have on your machine, installing the SDK could take a long time, from several minutes to a half hour or more.</span></span>
    > 
    > 

## <a name="download-the-sample-application"></a><span data-ttu-id="efe9a-133">De voorbeeldtoepassing downloaden</span><span class="sxs-lookup"><span data-stu-id="efe9a-133">Download the sample application</span></span>
1. <span data-ttu-id="efe9a-134">Download de opslagplaats [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list).</span><span class="sxs-lookup"><span data-stu-id="efe9a-134">Download the [Azure-Samples/app-service-api-dotnet-to-do-list](https://github.com/Azure-Samples/app-service-api-dotnet-todo-list) repository.</span></span>
   
    <span data-ttu-id="efe9a-135">U kunt klikken op de knop **ZIP downloaden** of de opslagplaats klonen op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="efe9a-135">You can click the **Download ZIP** button or clone the repository on your local machine.</span></span>
2. <span data-ttu-id="efe9a-136">Open de ToDoList-oplossing in Visual Studio 2015 of 2013.</span><span class="sxs-lookup"><span data-stu-id="efe9a-136">Open the ToDoList solution in Visual Studio 2015 or 2013.</span></span>
   
   1. <span data-ttu-id="efe9a-137">Het is belangrijk dat u elke oplossing vertrouwt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-137">You will need to trust each solution.</span></span>
         <span data-ttu-id="efe9a-138">![Beveiligingswaarschuwing](./media/app-service-api-dotnet-get-started/securitywarning.png)</span><span class="sxs-lookup"><span data-stu-id="efe9a-138">![Security Warning](./media/app-service-api-dotnet-get-started/securitywarning.png)</span></span>
3. <span data-ttu-id="efe9a-139">Maak de oplossing (CTRL + SHIFT + B) voor het herstellen van de NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="efe9a-139">Build the solution (CTRL + SHIFT + B)  to restore the NuGet packages.</span></span>
   
    <span data-ttu-id="efe9a-140">Als u de toepassing in actie wilt zien voordat u deze implementeert, kunt u deze lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="efe9a-140">If you want to see the application in operation before you deploy it, you can run it locally.</span></span> <span data-ttu-id="efe9a-141">Zorg ervoor dat ToDoListDataAPI uw opstartproject is en voer de oplossing uit.</span><span class="sxs-lookup"><span data-stu-id="efe9a-141">Make sure that ToDoListDataAPI is your startup project and run the solution.</span></span> <span data-ttu-id="efe9a-142">Er moet een 403 HTTP-fout in uw browser worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="efe9a-142">You should expect to see a HTTP 403 error in your browser.</span></span>

## <a name="use-swagger-api-metadata-and-ui"></a><span data-ttu-id="efe9a-143">Swagger API-metagegevens en -gebruikersinterface gebruiken</span><span class="sxs-lookup"><span data-stu-id="efe9a-143">Use Swagger API metadata and UI</span></span>
<span data-ttu-id="efe9a-144">Ondersteuning voor [Swagger](http://swagger.io/) 2.0 API-metagegevens is ingebouwd in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="efe9a-144">Support for [Swagger](http://swagger.io/) 2.0 API metadata is built into Azure App Service.</span></span> <span data-ttu-id="efe9a-145">Elke API-app kan een URL-eindpunt opgeven dat metagegevens retourneert voor de API in Swagger JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="efe9a-145">Each API app can specify a URL endpoint that returns metadata for the API in Swagger JSON format.</span></span> <span data-ttu-id="efe9a-146">De metagegevens die vanuit dat eindpunt worden geretourneerd, kunnen worden gebruikt voor het genereren van clientcode.</span><span class="sxs-lookup"><span data-stu-id="efe9a-146">The metadata returned from that endpoint can be used to generate client code.</span></span>

<span data-ttu-id="efe9a-147">Een ASP.NET Web API-project kan Swagger-metagegevens dynamisch genereren met behulp van het [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="efe9a-147">An ASP.NET Web API project can dynamically generate Swagger metadata by using the [Swashbuckle](https://www.nuget.org/packages/Swashbuckle) NuGet package.</span></span> <span data-ttu-id="efe9a-148">Het Swashbuckle NuGet-pakket is al geïnstalleerd in de ToDoListDataAPI- en ToDoListAPI-projecten die u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="efe9a-148">The Swashbuckle NuGet package is already installed in the ToDoListDataAPI and ToDoListAPI projects that you downloaded.</span></span>

<span data-ttu-id="efe9a-149">In deze sectie van de zelfstudie bekijkt u de gegenereerde Swagger 2.0-metagegevens en probeert u een testgebruikersinterface uit die hierop is gebaseerd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-149">In this section of the tutorial, you look at the generated Swagger 2.0 metadata, and then you try out a test UI that is based on the Swagger metadata.</span></span>

1. <span data-ttu-id="efe9a-150">Stel het project ToDoListDataAPI (**niet** het project ToDoListAPI) in als opstartproject.</span><span class="sxs-lookup"><span data-stu-id="efe9a-150">Set the ToDoListDataAPI project (**not** the ToDoListAPI project) as the startup project.</span></span>
   
    ![ToDoDataAPI instellen als opstartproject](./media/app-service-api-dotnet-get-started/startupproject.png)
2. <span data-ttu-id="efe9a-152">Druk op F5 of klik op **Fouten opsporen > Foutopsporing starten** om het project uit te voeren in de foutopsporingsmodus.</span><span class="sxs-lookup"><span data-stu-id="efe9a-152">Press F5 or click **Debug > Start Debugging** to run the project in debug mode.</span></span>
   
    <span data-ttu-id="efe9a-153">De browser wordt geopend en u ziet de foutpagina HTTP 403.</span><span class="sxs-lookup"><span data-stu-id="efe9a-153">The browser opens and shows the HTTP 403 error page.</span></span>
3. <span data-ttu-id="efe9a-154">Voeg in de adresbalk van uw browser `swagger/docs/v1` toe aan het einde van de regel en druk vervolgens op Enter.</span><span class="sxs-lookup"><span data-stu-id="efe9a-154">In your browser address bar, add `swagger/docs/v1` to the end of the line, and then press Return.</span></span> <span data-ttu-id="efe9a-155">(De URL is `http://localhost:45914/swagger/docs/v1`.)</span><span class="sxs-lookup"><span data-stu-id="efe9a-155">(The URL is `http://localhost:45914/swagger/docs/v1`.)</span></span>
   
    <span data-ttu-id="efe9a-156">Dit is de standaard-URL die wordt gebruikt om Swashbuckle Swagger 2.0 JSON-metagegevens te retourneren voor de API.</span><span class="sxs-lookup"><span data-stu-id="efe9a-156">This is the default URL used by Swashbuckle to return Swagger 2.0 JSON metadata for the API.</span></span>
   
    <span data-ttu-id="efe9a-157">Als u Internet Explorer gebruikt, vraagt de browser u om een *v1.json*-bestand te downloaden.</span><span class="sxs-lookup"><span data-stu-id="efe9a-157">If you're using Internet Explorer, the browser prompts you to download a *v1.json* file.</span></span>
   
    ![JSON-metagegevens downloaden in Internet Explorer](./media/app-service-api-dotnet-get-started/iev1json.png)
   
    <span data-ttu-id="efe9a-159">Als u Chrome, Firefox of Edge gebruikt, wordt de JSON-code rechtstreeks in een browservenster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="efe9a-159">If you're using Chrome, Firefox, or Edge, the browser displays the JSON in the browser window.</span></span> <span data-ttu-id="efe9a-160">Verschillende browsers verwerken JSON op een verschillende manier. Mogelijk ziet uw browservenster er daarom niet precies hetzelfde uit als in het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="efe9a-160">Different browsers handle JSON differently, and your browser window may not look exactly like the example.</span></span>
   
    ![JSON-metagegevens in Chrome](./media/app-service-api-dotnet-get-started/chromev1json.png)
   
    <span data-ttu-id="efe9a-162">Het volgende voorbeeld toont de eerste sectie van de Swagger-metagegevens voor de API, met de definitie voor de Get-methode.</span><span class="sxs-lookup"><span data-stu-id="efe9a-162">The following sample shows the first section of the Swagger metadata for the API, with the definition for the Get method.</span></span> <span data-ttu-id="efe9a-163">Deze metagegevens sturen de Swagger-gebruikersinterface aan die u in de volgende stappen nodig hebt. U gebruikt deze verderop in de zelfstudie voor het automatisch genereren van clientcode.</span><span class="sxs-lookup"><span data-stu-id="efe9a-163">This metadata is what drives the Swagger UI that you use in the following steps, and you use it in a later section of the tutorial to automatically generate client code.</span></span>
   
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
4. <span data-ttu-id="efe9a-164">Sluit de browser en stop de foutopsporing van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="efe9a-164">Close the browser and stop Visual Studio debugging.</span></span>
5. <span data-ttu-id="efe9a-165">Open in het project ToDoListDataAPI in **Solution Explorer** het bestand *App_Start\SwaggerConfig.cs*, blader naar regel 174 en verwijder het commentaarteken bij de volgende code.</span><span class="sxs-lookup"><span data-stu-id="efe9a-165">In the ToDoListDataAPI project in **Solution Explorer**, open the *App_Start\SwaggerConfig.cs* file, then scroll down to line 174 and uncomment the following code.</span></span>
   
        /*
            })
        .EnableSwaggerUi(c =>
            {
        */
   
    <span data-ttu-id="efe9a-166">Het bestand *SwaggerConfig.cs* wordt gemaakt wanneer u het pakket Swashbuckle in een project installeert.</span><span class="sxs-lookup"><span data-stu-id="efe9a-166">The *SwaggerConfig.cs* file is created when you install the Swashbuckle package in a project.</span></span> <span data-ttu-id="efe9a-167">Het bestand biedt diverse manieren om Swashbuckle te configureren.</span><span class="sxs-lookup"><span data-stu-id="efe9a-167">The file provides a number of ways to configure Swashbuckle.</span></span>
   
    <span data-ttu-id="efe9a-168">Met de code waarbij u het commentaarteken hebt verwijderd, wordt de Swagger-gebruikersinterface ingeschakeld die u in de volgende stappen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-168">The code you've uncommented enables the Swagger UI that you use in the following steps.</span></span> <span data-ttu-id="efe9a-169">Wanneer u een Web API-project maakt met behulp van de API-app-projectsjabloon, wordt deze code als veiligheidsmaatregel standaard uitgecommentarieerd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-169">When you create a Web API project by using the API app project template, this code is commented out by default as a security measure.</span></span>
6. <span data-ttu-id="efe9a-170">Voer het project opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="efe9a-170">Run the project again.</span></span>
7. <span data-ttu-id="efe9a-171">Voeg in de adresbalk van uw browser `swagger` toe aan het einde van de regel en druk vervolgens op Enter.</span><span class="sxs-lookup"><span data-stu-id="efe9a-171">In your browser address bar, add `swagger` to the end of the line, and then press Return.</span></span> <span data-ttu-id="efe9a-172">(De URL is `http://localhost:45914/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="efe9a-172">(The URL is `http://localhost:45914/swagger`.)</span></span>
8. <span data-ttu-id="efe9a-173">Wanneer de pagina van de Swagger-gebruikersinterface wordt weergegeven, klikt u op **ToDoList** om na te gaan welke methoden er beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="efe9a-173">When the Swagger UI page appears, click **ToDoList** to see the methods available.</span></span>
   
    ![Beschikbare methoden in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/methods.png)
9. <span data-ttu-id="efe9a-175">Klik op de eerste knop **Get** in de lijst.</span><span class="sxs-lookup"><span data-stu-id="efe9a-175">Click the first **Get** button in the list.</span></span>
10. <span data-ttu-id="efe9a-176">Geef in de sectie **Parameters** een sterretje op als de waarde van de `owner`-parameter en klik vervolgens op **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-176">In the **Parameters** section, enter an asterisk as the value of the `owner` parameter, and then click **Try it out**.</span></span>
    
    <span data-ttu-id="efe9a-177">Als u in latere zelfstudies verificatie toevoegt, biedt de middelste laag de werkelijke gebruikers-id voor de gegevenslaag.</span><span class="sxs-lookup"><span data-stu-id="efe9a-177">When you add authentication in later tutorials, the middle tier will provide the actual user ID to the data tier.</span></span> <span data-ttu-id="efe9a-178">Zolang de toepassing wordt uitgevoerd zonder dat verificatie is ingeschakeld, hebben alle taken een sterretje als eigenaar-id.</span><span class="sxs-lookup"><span data-stu-id="efe9a-178">For now, all tasks will have asterisk as their owner ID while the application runs without authentication enabled.</span></span>
    
    ![Try it out in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/gettryitout1.png)
    
    <span data-ttu-id="efe9a-180">De Swagger-gebruikersinterface roept deToDoList Get-methode aan en geeft de responscode en JSON-resultaten weer.</span><span class="sxs-lookup"><span data-stu-id="efe9a-180">The Swagger UI calls the ToDoList Get method and displays the response code and JSON results.</span></span>
    
    ![Resultaten van Try it out in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/gettryitout.png)
11. <span data-ttu-id="efe9a-182">Klik op **Post** en vervolgens op het vak onder **Model Schema**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-182">Click **Post**, and then click the box under **Model Schema**.</span></span>
    
    <span data-ttu-id="efe9a-183">Als u op het modelschema klikt, worden er gegevens ingevuld in het invoervak waarin u de waarde van parameter voor de Post-methode kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="efe9a-183">Clicking the model schema prefills the input box where you can specify the parameter value for the Post method.</span></span> <span data-ttu-id="efe9a-184">(Als dit in Internet Explorer niet werkt, probeert u een andere browser of voert u in de volgende stap de waarde van de parameter handmatig in.)</span><span class="sxs-lookup"><span data-stu-id="efe9a-184">(If this doesn't work in Internet Explorer, use a different browser or enter the parameter value manually in the next step.)</span></span>  
    
    ![Post voor Try it out in de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/post.png)
12. <span data-ttu-id="efe9a-186">Wijzig de JSON-code in het invoervak van de `todo`-parameter, zodat deze lijkt op het volgende voorbeeld of vervang deze door uw eigen beschrijvende tekst:</span><span class="sxs-lookup"><span data-stu-id="efe9a-186">Change the JSON in the `todo` parameter input box so that it looks like the following example, or substitute your own description text:</span></span>
    
        {
          "ID": 2,
          "Description": "buy the dog a toy",
          "Owner": "*"
        }
13. <span data-ttu-id="efe9a-187">Klik op **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-187">Click **Try it out**.</span></span>
    
    <span data-ttu-id="efe9a-188">De ToDoList-API retourneert een 204 HTTP-responscode waarmee wordt aangegeven dat de bewerking is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-188">The ToDoList API returns an HTTP 204 response code that indicates success.</span></span>
14. <span data-ttu-id="efe9a-189">Klik op de eerste **Get**-knop en klik vervolgens in die sectie van de pagina op de knop **Try it out**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-189">Click the first **Get** button, and then in that section of the page click the **Try it out** button.</span></span>
    
    <span data-ttu-id="efe9a-190">De respons van de Get-methode bevat nu de nieuwe taak.</span><span class="sxs-lookup"><span data-stu-id="efe9a-190">The Get method response now includes the new to do item.</span></span>
15. <span data-ttu-id="efe9a-191">Optioneel: probeer ook de methoden Put, Delete en Get by ID.</span><span class="sxs-lookup"><span data-stu-id="efe9a-191">Optional: Try also the Put, Delete, and Get by ID methods.</span></span>
16. <span data-ttu-id="efe9a-192">Sluit de browser en stop de foutopsporing van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="efe9a-192">Close the browser and stop Visual Studio debugging.</span></span>

<span data-ttu-id="efe9a-193">Swashbuckle werkt met elk ASP.NET Web API-project.</span><span class="sxs-lookup"><span data-stu-id="efe9a-193">Swashbuckle works with any ASP.NET Web API project.</span></span> <span data-ttu-id="efe9a-194">Als u het genereren van Swagger-metagegevens wilt toevoegen aan een bestaand project, hoeft u hiervoor alleen het Swashbuckle-pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="efe9a-194">If you want to add Swagger metadata generation to an existing project, just install the Swashbuckle package.</span></span>

> [!NOTE]
> <span data-ttu-id="efe9a-195">De Swagger-metagegevens bevatten voor elke API-bewerking een unieke id.</span><span class="sxs-lookup"><span data-stu-id="efe9a-195">Swagger metadata includes a unique ID for each API operation.</span></span> <span data-ttu-id="efe9a-196">Standaard kan Swashbuckle dubbele Swagger-bewerkings-id's genereren voor uw Web API-controllermethoden.</span><span class="sxs-lookup"><span data-stu-id="efe9a-196">By default, Swashbuckle may generate duplicate Swagger operation IDs for your Web API controller methods.</span></span> <span data-ttu-id="efe9a-197">Dit gebeurt als uw domeincontroller overbelaste HTTP-methoden bevat, zoals `Get()` en `Get(id)`.</span><span class="sxs-lookup"><span data-stu-id="efe9a-197">This happens if your controller has overloaded HTTP methods, such as `Get()` and `Get(id)`.</span></span> <span data-ttu-id="efe9a-198">Zie [Door Swashbuckle gegenereerde API-definities aanpassen](app-service-api-dotnet-swashbuckle-customize.md) voor meer informatie over het afhandelen van overbelasting.</span><span class="sxs-lookup"><span data-stu-id="efe9a-198">For information about how to handle overloads, see [Customize Swashbuckle-generated API definitions](app-service-api-dotnet-swashbuckle-customize.md).</span></span> <span data-ttu-id="efe9a-199">Als u in Visual Studio een Web API-project maakt met de Azure-API-app-sjabloon, wordt er aan het bestand *SwaggerConfig.cs* automatisch code toegevoegd die unieke bewerkings-id's geneert.</span><span class="sxs-lookup"><span data-stu-id="efe9a-199">If you create a Web API project in Visual Studio by using the Azure API App template, code that generates unique operation IDs is automatically added to the *SwaggerConfig.cs* file.</span></span>  
> 
> 

## <span data-ttu-id="efe9a-200"><a id="createapiapp"></a> Een API-app in Azure maken en er code in implementeren</span><span class="sxs-lookup"><span data-stu-id="efe9a-200"><a id="createapiapp"></a> Create an API app in Azure and deploy code to it</span></span>
<span data-ttu-id="efe9a-201">In deze sectie gebruikt u de Azure-hulpprogramma's die in de wizard **Publish Web** van Visual Studio zijn geïntegreerd, voor het maken van een nieuwe API-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="efe9a-201">In this section, you use Azure tools that are integrated into the Visual Studio **Publish Web** wizard to create a new API app in Azure.</span></span> <span data-ttu-id="efe9a-202">Vervolgens implementeert u het project ToDoListDataAPI in de nieuwe API-app en roept u de API aan door de Swagger-gebruikersinterface uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="efe9a-202">Then you deploy the ToDoListDataAPI project to the new API app and call the API by running the Swagger UI.</span></span>

1. <span data-ttu-id="efe9a-203">Klik in **Solution Explorer** met de rechtermuisknop op het project ToDoListDataAPI. Klik vervolgens op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-203">In **Solution Explorer**, right-click the ToDoListDataAPI project, and then click **Publish**.</span></span>
   
    ![Klikken op Publish in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu.png)
2. <span data-ttu-id="efe9a-205">Klik in de stap **Profile** van de wizard **Publish Web** op **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-205">In the **Profile** step of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
   
   ![Klikken op Azure App Service in de wizard Publish Web](./media/app-service-api-dotnet-get-started/selectappservice.png)
3. <span data-ttu-id="efe9a-207">Meld u aan bij uw Azure-account als u dit nog niet hebt gedaan. Vernieuw uw referenties als deze zijn verlopen.</span><span class="sxs-lookup"><span data-stu-id="efe9a-207">Sign in to your Azure account if you have not already done so, or refresh your credentials if they're expired.</span></span>
4. <span data-ttu-id="efe9a-208">Kies in het dialoogvenster App Service bij **Subscription** het Azure-abonnement dat u wilt gebruiken en klik vervolgens op **New**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-208">In the App Service dialog box, choose the Azure **Subscription** you want to use, and then click **New**.</span></span>
   
    ![Klikken op New in het dialoogvenster App Service](./media/app-service-api-dotnet-get-started/clicknew.png)
   
    <span data-ttu-id="efe9a-210">Het tabblad **Hosting** van het dialoogvenster **Create App Service** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="efe9a-210">The **Hosting** tab of the **Create App Service** dialog box appears.</span></span>
   
    <span data-ttu-id="efe9a-211">Omdat u een Web API-project implementeert waarin Swashbuckle is geïnstalleerd, neemt Visual Studio aan dat u een API-app wilt maken.</span><span class="sxs-lookup"><span data-stu-id="efe9a-211">Because you're deploying a Web API project that has Swashbuckle installed, Visual Studio assumes that you want to create an API App.</span></span> <span data-ttu-id="efe9a-212">Dit wordt aangegeven door de titel **API App Name** en door het feit dat de vervolgkeuzelijst **Change Type** is ingesteld op **API App**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-212">This is indicated by the **API App Name** title and by the fact that the **Change Type** drop-down list is set to **API App**.</span></span>
   
    ![App-type in het dialoogvenster App Service](./media/app-service-api-dotnet-get-started/apptype.png)
5. <span data-ttu-id="efe9a-214">Voer bij **API App Name** een naam in die uniek is in het domein *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="efe9a-214">Enter an **API App Name** that is unique in the *azurewebsites.net* domain.</span></span> <span data-ttu-id="efe9a-215">U kunt de standaardnaam accepteren die door Visual Studio wordt voorgesteld.</span><span class="sxs-lookup"><span data-stu-id="efe9a-215">You can accept the default name that Visual Studio proposes.</span></span>
   
    <span data-ttu-id="efe9a-216">Als u een naam opgeeft die iemand anders al gebruikt, ziet u aan de rechterkant een rood uitroepteken.</span><span class="sxs-lookup"><span data-stu-id="efe9a-216">If you enter a name that someone else has already used, you see a red exclamation mark to the right.</span></span>
   
    <span data-ttu-id="efe9a-217">De URL van de API-app wordt `{API app name}.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="efe9a-217">The URL of the API app will be `{API app name}.azurewebsites.net`.</span></span>
6. <span data-ttu-id="efe9a-218">Klik in de vervolgkeuzelijst **Resource Group** op **New** en voer vervolgens ToDoListGroup of desgewenst een andere naam in.</span><span class="sxs-lookup"><span data-stu-id="efe9a-218">In the **Resource Group** drop-down, click **New**, and then enter "ToDoListGroup" or another name if you prefer.</span></span>
   
    <span data-ttu-id="efe9a-219">Een resourcegroep is een verzameling Azure-resources, zoals web-apps, databases, virtuele machines, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="efe9a-219">A resource group is a collection of Azure resources such as API apps, databases, VMs, and so forth.</span></span>    <span data-ttu-id="efe9a-220">Voor deze zelfstudie kunt u het beste een nieuwe resourcegroep maken. U kunt dan eenvoudig in één stap alle Azure-resources verwijderen die u tijdens de zelfstudie maakt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-220">For this tutorial, it's best to create a new resource group because that makes it easy to delete in one step all the Azure resources that you create for the tutorial.</span></span>
   
    <span data-ttu-id="efe9a-221">In dit vak kunt u een bestaande [resourcegroep](../azure-resource-manager/resource-group-overview.md) selecteren of een nieuwe maken door een naam te typen die anders is dan alle bestaande resourcegroepen in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="efe9a-221">This box lets you select an existing [resource group](../azure-resource-manager/resource-group-overview.md) or create a new one by typing in a name that is different from any existing resource group in your subscription.</span></span>
7. <span data-ttu-id="efe9a-222">Klik naast de vervolgkeuzelijst **App Service Plan** op de knop **New**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-222">Click the **New** button next to the **App Service Plan** drop-down.</span></span>
   
    <span data-ttu-id="efe9a-223">De schermafbeelding toont voorbeeldwaarden voor **API App Name**, **Subscription** en **Resource Group**. De door u gebruikte waarden zijn anders.</span><span class="sxs-lookup"><span data-stu-id="efe9a-223">The screen shot shows sample values for **API App Name**, **Subscription**, and **Resource Group** -- your values will be different.</span></span>
   
    ![Het dialoogvenster Create App Service](./media/app-service-api-dotnet-get-started/createas.png)
   
    <span data-ttu-id="efe9a-225">In de volgende stappen maakt u een App Service-plan voor de nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="efe9a-225">In the following steps you create an App Service plan for the new resource group.</span></span> <span data-ttu-id="efe9a-226">In een App Service-plan worden de rekenresources opgegeven op basis waarvan uw API-app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-226">An App Service plan specifies the compute resources that your API app runs on.</span></span> <span data-ttu-id="efe9a-227">Als u bijvoorbeeld de gratis categorie hebt gekozen, wordt uw API-app uitgevoerd op basis van gedeelde virtuele machines. Bij sommige categorieën waar u voor betaalt, worden apps uitgevoerd via exclusieve virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="efe9a-227">For example, if you choose the free tier, your API app runs on shared VMs, while for some paid tiers it runs on dedicated VMs.</span></span> <span data-ttu-id="efe9a-228">Zie [Overzicht van App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) voor informatie over App Service-plannen</span><span class="sxs-lookup"><span data-stu-id="efe9a-228">For information about App Service plans, see [App Service plans overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
8. <span data-ttu-id="efe9a-229">Geef in het dialoogvenster **Configure App Service Plan** de naam ToDoListPlan op. Desgewenst kunt u ook een andere naam gebruiken.</span><span class="sxs-lookup"><span data-stu-id="efe9a-229">In the **Configure App Service Plan** dialog, enter "ToDoListPlan" or another name if you prefer.</span></span>
9. <span data-ttu-id="efe9a-230">Kies in de vervolgkeuzelijst **Location** de locatie die het dichtst bij u ligt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-230">In the **Location** drop-down list, choose the location that is closest to you.</span></span>
   
    <span data-ttu-id="efe9a-231">Met deze instelling bepaalt u in welk Azure-datacentrum uw app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-231">This setting specifies which Azure datacenter your app will run in.</span></span> <span data-ttu-id="efe9a-232">Kies een locatie dicht bij u in de buurt om de [latentie](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090) te minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="efe9a-232">Choose a location close to you to minimize [latency](http://www.bing.com/search?q=web%20latency%20introduction&qs=n&form=QBRE&pq=web%20latency%20introduction&sc=1-24&sp=-1&sk=&cvid=eefff99dfc864d25a75a83740f1e0090).</span></span>
10. <span data-ttu-id="efe9a-233">Klik in de vervolgkeuzelijst **Size** op **Free**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-233">In the **Size** drop-down, click **Free**.</span></span>
    
    <span data-ttu-id="efe9a-234">Voor deze zelfstudie levert de prijscategorie Free voldoende prestaties.</span><span class="sxs-lookup"><span data-stu-id="efe9a-234">For this tutorial, the free pricing tier will provide sufficient performance.</span></span>
11. <span data-ttu-id="efe9a-235">Klik in het dialoogvenster **Configure App Service Plan** op **OK**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-235">In the **Configure App Service Plan** dialog, click **OK**.</span></span>
    
    ![Klikken op OK in het dialoogvenster Configure App Service Plan](./media/app-service-api-dotnet-get-started/configasp.png)
12. <span data-ttu-id="efe9a-237">Klik in het dialoogvenster **Create App Service** op **Create**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-237">In the **Create App Service** dialog box, click **Create**.</span></span>
    
    ![Klikken op Create in het dialoogvenster Create App Service](./media/app-service-api-dotnet-get-started/clickcreate.png)
    
    <span data-ttu-id="efe9a-239">Visual Studio maakt de API-app en een publicatieprofiel met alle vereiste instellingen voor de API-app.</span><span class="sxs-lookup"><span data-stu-id="efe9a-239">Visual Studio creates the API app and a publish profile that has all of the required settings for the API app.</span></span> <span data-ttu-id="efe9a-240">Vervolgens wordt de wizard **Publish Web** geopend. Deze wizard gebruikt u voor het implementeren van het project.</span><span class="sxs-lookup"><span data-stu-id="efe9a-240">Then it opens the **Publish Web** wizard, which you'll use to deploy the project.</span></span>
    
    <span data-ttu-id="efe9a-241">De wizard **Publish Web** wordt geopend op het tabblad **Connection** (hieronder getoond).</span><span class="sxs-lookup"><span data-stu-id="efe9a-241">The **Publish Web** wizard opens on the **Connection** tab (shown below).</span></span>
    
    <span data-ttu-id="efe9a-242">Op het tabblad **Connection** verwijzen de instellingen bij **Server** en **Site name** naar uw API-app.</span><span class="sxs-lookup"><span data-stu-id="efe9a-242">On the **Connection** tab, the **Server** and **Site name** settings point to your API app.</span></span> <span data-ttu-id="efe9a-243">**User name** en **Password** zijn implementatiereferenties die Azure voor u maakt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-243">The **User name** and **Password** are deployment credentials that Azure creates for you.</span></span> <span data-ttu-id="efe9a-244">Na de implementatie opent Visual Studio een browservenster met de **doel-URL** (dat is de enige functie van **doel-URL**).</span><span class="sxs-lookup"><span data-stu-id="efe9a-244">After deployment, Visual Studio opens a browser to the **Destination URL** (that's the only purpose for **Destination URL**).</span></span>  
13. <span data-ttu-id="efe9a-245">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-245">Click **Next**.</span></span>
    
    ![Klikken op Next op het tabblad Connection van de wizard Publish Web](./media/app-service-api-dotnet-get-started/connnext.png)
    
    <span data-ttu-id="efe9a-247">Het volgende tabblad is het tabblad **Settings** (hieronder getoond).</span><span class="sxs-lookup"><span data-stu-id="efe9a-247">The next tab is the **Settings** tab (shown below).</span></span> <span data-ttu-id="efe9a-248">Hier kunt u het buildconfiguratietabblad wijzigen om een build voor foutopsporing te implementeren voor [foutopsporing op afstand](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span><span class="sxs-lookup"><span data-stu-id="efe9a-248">Here you can change the build configuration tab to deploy a debug build for [remote debugging](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug).</span></span> <span data-ttu-id="efe9a-249">Het tabblad biedt ook diverse **opties voor het publiceren van bestanden**:</span><span class="sxs-lookup"><span data-stu-id="efe9a-249">The tab also offers several **File Publish Options**:</span></span>
    
    * <span data-ttu-id="efe9a-250">Aanvullende bestanden op de bestemming verwijderen</span><span class="sxs-lookup"><span data-stu-id="efe9a-250">Remove additional files at destination</span></span>
    * <span data-ttu-id="efe9a-251">Voorcompileren tijdens het publiceren</span><span class="sxs-lookup"><span data-stu-id="efe9a-251">Precompile during publishing</span></span>
    * <span data-ttu-id="efe9a-252">Bestanden uitsluiten van de map App_Data</span><span class="sxs-lookup"><span data-stu-id="efe9a-252">Exclude files from the App_Data folder</span></span>
    
    <span data-ttu-id="efe9a-253">Voor deze zelfstudie hebt u geen van deze opties nodig.</span><span class="sxs-lookup"><span data-stu-id="efe9a-253">For this tutorial you don't need any of these.</span></span> <span data-ttu-id="efe9a-254">Zie [Procedure: een webproject implementeren met behulp van publicatie met één klik in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx) voor gedetailleerde uitleg over deze opties.</span><span class="sxs-lookup"><span data-stu-id="efe9a-254">For detailed explanations of what they do, see [How to: Deploy a Web Project Using One-Click Publish in Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx).</span></span>
14. <span data-ttu-id="efe9a-255">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-255">Click **Next**.</span></span>
    
    ![Klikken op Next op het tabblad Settings van de wizard Publish Web](./media/app-service-api-dotnet-get-started/settingsnext.png)
    
    <span data-ttu-id="efe9a-257">Hierna volgt het tabblad **Preview** (hieronder getoond), waar u kunt bekijken welke bestanden van uw project er naar de API-app worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-257">Next is the **Preview** tab (shown below), which gives you an opportunity to see what files are going to be copied from your project to the API app.</span></span> <span data-ttu-id="efe9a-258">Wanneer u een project implementeert in een API-app die u al eerder had geïmplementeerd, worden alleen de gewijzigde bestanden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-258">When you're deploying a project to an API app that you already deployed to earlier, only changed files are copied.</span></span> <span data-ttu-id="efe9a-259">Als u een overzicht wilt zien van wat er wordt gekopieerd, klikt u op de knop **Start Preview**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-259">If you want to see a list of what will be copied, you can click the **Start Preview** button.</span></span>
15. <span data-ttu-id="efe9a-260">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-260">Click **Publish**.</span></span>
    
    ![Klikken op Publish op het tabblad Preview van de wizard Publish Web](./media/app-service-api-dotnet-get-started/clickpublish.png)
    
    <span data-ttu-id="efe9a-262">Visual Studio implementeert het project ToDoListDataAPI in de nieuwe API-app.</span><span class="sxs-lookup"><span data-stu-id="efe9a-262">Visual Studio deploys the ToDoListDataAPI project to the new API app.</span></span> <span data-ttu-id="efe9a-263">In het venster **Output** wordt bevestigd dat de implementatie is geslaagd. Ook wordt de URL van de API-app in een browservenster geopend, waarna er een pagina wordt weergegeven met de melding dat de nieuwe API-app is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-263">The **Output** window logs successful deployment, and a "successfully created" page appears in a browser window opened to the URL of the API app.</span></span>
    
    ![Bevestiging van geslaagde implementatie in het venster Output](./media/app-service-api-dotnet-get-started/deploymentoutput.png)
    
    ![Pagina met melding dat de nieuwe API-app is gemaakt](./media/app-service-api-dotnet-get-started/appcreated.png)
16. <span data-ttu-id="efe9a-266">Voeg 'swagger' toe aan de URL in de adresbalk van de browser en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="efe9a-266">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="efe9a-267">(De URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="efe9a-267">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
    
    <span data-ttu-id="efe9a-268">De browser geeft dezelfde Swagger-gebruikersinterface weer die u eerder hebt gezien, maar deze wordt nu uitgevoerd in de cloud.</span><span class="sxs-lookup"><span data-stu-id="efe9a-268">The browser displays the same Swagger UI that you saw earlier, but now it's running in the cloud.</span></span> <span data-ttu-id="efe9a-269">Probeer de Get-methode uit en u zult zien dat u bent teruggekeerd naar de twee standaardtaken.</span><span class="sxs-lookup"><span data-stu-id="efe9a-269">Try out the Get method, and you see that you're back to the default 2 to-do items.</span></span> <span data-ttu-id="efe9a-270">De wijzigingen die u eerder hebt doorgevoerd, zijn in het geheugen van de lokale computer opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="efe9a-270">The changes you made earlier were saved in memory in the local machine.</span></span>
17. <span data-ttu-id="efe9a-271">Open de [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="efe9a-271">Open the [Azure portal](https://portal.azure.com/).</span></span>
    
    <span data-ttu-id="efe9a-272">Azure Portal is een webinterface voor het beheer van Azure-bronnen zoals API-apps.</span><span class="sxs-lookup"><span data-stu-id="efe9a-272">The Azure portal is a web interface for managing Azure resources such as API apps.</span></span>
18. <span data-ttu-id="efe9a-273">Klik op **Meer Services > App Services**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-273">Click **More Services > App Services**.</span></span>
    
    ![Bladeren door App Services](./media/app-service-api-dotnet-get-started/browseas.png)
19. <span data-ttu-id="efe9a-275">Zoek uw nieuwe API-app op op de blade **App Services** en klik erop.</span><span class="sxs-lookup"><span data-stu-id="efe9a-275">In the **App Services** blade, find and click your new API app.</span></span> <span data-ttu-id="efe9a-276">(In Azure Portal worden de vensters die aan de rechterkant worden geopend, *blades* genoemd.)</span><span class="sxs-lookup"><span data-stu-id="efe9a-276">(In the Azure portal, windows that open to the right are called *blades*.)</span></span>
    
    ![De blade App Services](./media/app-service-api-dotnet-get-started/choosenewapiappinportal.png)
    
    <span data-ttu-id="efe9a-278">Er worden twee blades geopend.</span><span class="sxs-lookup"><span data-stu-id="efe9a-278">Two blades open.</span></span> <span data-ttu-id="efe9a-279">De eerste blade bevat een overzicht van de API-app. De tweede bevat een lange lijst met instellingen die u kunt bekijken en wijzigen.</span><span class="sxs-lookup"><span data-stu-id="efe9a-279">One blade has an overview of the API app, and one has a long list of settings that you can view and change.</span></span>
20. <span data-ttu-id="efe9a-280">Ga op de blade **Instellingen** naar de sectie **API** en klik op **API-definitie**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-280">In the **Settings** blade, find the **API** section and click **API Definition**.</span></span>
    
    ![API-definitie op de blade Instellingen](./media/app-service-api-dotnet-get-started/apidefinsettings.png)
    
    <span data-ttu-id="efe9a-282">Op de blade **API-definitie** kunt u de URL opgeven die de Swagger 2.0-metagegevens in JSON-indeling retourneert.</span><span class="sxs-lookup"><span data-stu-id="efe9a-282">The **API Definition** blade lets you specify the URL that returns Swagger 2.0 metadata in JSON format.</span></span> <span data-ttu-id="efe9a-283">Wanneer Visual Studio de API-app maakt, wordt de URL van de API-definitie ingesteld op de standaardwaarde voor door Swashbuckle gegenereerde metagegevens die u eerder hebt gezien. Dit zijn de basis-URL van de API-app plus `/swagger/docs/v1`.</span><span class="sxs-lookup"><span data-stu-id="efe9a-283">When Visual Studio creates the API app, it sets the API definition URL to the default value for Swashbuckle-generated metadata that you saw earlier, which is the API app's base URL plus `/swagger/docs/v1`.</span></span>
    
    ![URL van de API-definitie](./media/app-service-api-dotnet-get-started/apidefurl.png)
    
    <span data-ttu-id="efe9a-285">Wanneer u een API-app selecteert om er clientcode voor te genereren, worden de metagegevens door Visual Studio opgehaald via deze URL.</span><span class="sxs-lookup"><span data-stu-id="efe9a-285">When you select an API app to generate client code for it, Visual Studio retrieves the metadata from this URL.</span></span>

## <span data-ttu-id="efe9a-286"><a id="codegen"></a> Clientcode genereren voor de gegevenslaag</span><span class="sxs-lookup"><span data-stu-id="efe9a-286"><a id="codegen"></a> Generate client code for the data tier</span></span>
<span data-ttu-id="efe9a-287">Een van de voordelen van de integratie van Swagger in Azure API-apps is het automatisch genereren van code.</span><span class="sxs-lookup"><span data-stu-id="efe9a-287">One of the advantages of integrating Swagger into Azure API apps is automatic code generation.</span></span> <span data-ttu-id="efe9a-288">Gegenereerde clientklassen maken het gemakkelijker code te schrijven die een API-app aanroepen.</span><span class="sxs-lookup"><span data-stu-id="efe9a-288">Generated client classes make it easier to write code that calls an API app.</span></span>

<span data-ttu-id="efe9a-289">Het project ToDoListAPI heeft de gegenereerde clientcode al, maar in de volgende stappen gaat u deze verwijderen en opnieuw genereren om te leren hoe dit in zijn werk gaat.</span><span class="sxs-lookup"><span data-stu-id="efe9a-289">The ToDoListAPI project already has the generated client code, but in the following steps you'll delete it and regenerate it to see how to do the code generation.</span></span>

1. <span data-ttu-id="efe9a-290">Verwijder in Visual Studio **Solution Explorer** in het project ToDoListAPI de map *ToDoListDataAPI*.</span><span class="sxs-lookup"><span data-stu-id="efe9a-290">In Visual Studio **Solution Explorer**, in the ToDoListAPI project, delete the *ToDoListDataAPI* folder.</span></span> <span data-ttu-id="efe9a-291">**Waarschuwing: verwijder alleen de map, niet het project ToDoListDataAPI.**</span><span class="sxs-lookup"><span data-stu-id="efe9a-291">**Caution: Delete only the folder, not the ToDoListDataAPI project.**</span></span>
   
    ![Gegenereerde clientcode verwijderen](./media/app-service-api-dotnet-get-started/deletecodegen.png)
   
    <span data-ttu-id="efe9a-293">Deze map is gemaakt met behulp van het proces voor het genereren van code dat u zo dadelijk gaat doorlopen.</span><span class="sxs-lookup"><span data-stu-id="efe9a-293">This folder was created by using the code generation process that you're about to go through.</span></span>
2. <span data-ttu-id="efe9a-294">Klik met de rechtermuisknop op het project ToDoListAPI en klik vervolgens op **Add > REST API Client**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-294">Right-click the ToDoListAPI project, and then click **Add > REST API Client**.</span></span>
   
    ![REST-API-client toevoegen in Visual Studio](./media/app-service-api-dotnet-get-started/codegenmenu.png)
3. <span data-ttu-id="efe9a-296">Klik in het dialoogvenster **Add REST API Client** op **Swagger URL**. Klik vervolgens op **Select Azure Asset**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-296">In the **Add REST API Client** dialog box, click **Swagger URL**, and then click **Select Azure Asset**.</span></span>
   
    ![Azure-asset selecteren](./media/app-service-api-dotnet-get-started/codegenbrowse.png)
4. <span data-ttu-id="efe9a-298">Vouw in het dialoogvenster **App Service** de resourcegroep uit die u voor deze zelfstudie gebruikt en selecteer uw API-app. Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-298">In the **App Service** dialog box, expand the resource group you're using for this tutorial and select your API app, and then click **OK**.</span></span>
   
    ![API-app selecteren voor het genereren van code](./media/app-service-api-dotnet-get-started/codegenselect.png)
   
    <span data-ttu-id="efe9a-300">Als u terugkeert naar het dialoogvenster **Add REST API Client**, zult u zien dat in het tekstvak de URL-waarde van de API-definitie die u eerder in de portal zag, is ingevuld.</span><span class="sxs-lookup"><span data-stu-id="efe9a-300">Notice that when you return to the **Add REST API Client** dialog, the text box has been filled in with the API definition URL value that you saw earlier in the portal.</span></span>
   
    ![URL van de API-definitie](./media/app-service-api-dotnet-get-started/codegenurlplugged.png)
   
   > [!TIP]
   > <span data-ttu-id="efe9a-302">Behalve via het bladerdialoogvenster kunt u de metagegevens voor het genereren van code ook ophalen door de URL direct in te voeren.</span><span class="sxs-lookup"><span data-stu-id="efe9a-302">An alternative way to get metadata for code generation is to enter the URL directly instead of going through the browse dialog.</span></span> <span data-ttu-id="efe9a-303">Als u clientcode wilt genereren voordat u Azure implementeert, kunt u bovendien ook het volgende doen: voer het Web API-project lokaal uit, ga naar de URL die het Swagger JSON-bestand aanlevert, sla het bestand op en selecteer de optie **Select an existing Swagger metadata file**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-303">Or if you want to generate client code before deploying to Azure, you could run the Web API project locally, go to the URL that provides the Swagger JSON file, save the file, and use the **Select an existing Swagger metadata file** option.</span></span>
   > 
   > 
5. <span data-ttu-id="efe9a-304">Klik in het dialoogvenster **Add REST API Client** op **OK**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-304">In the **Add REST API Client** dialog box, click **OK**.</span></span>
   
    <span data-ttu-id="efe9a-305">Visual Studio maakt een map met de naam van de API-app en genereert clientklassen.</span><span class="sxs-lookup"><span data-stu-id="efe9a-305">Visual Studio creates a folder named after the API app and generates client classes.</span></span>
   
    ![Codebestanden voor gegenereerde client](./media/app-service-api-dotnet-get-started/codegenfiles.png)
6. <span data-ttu-id="efe9a-307">Open in het project ToDoListAPI *Controllers\ToDoListController.cs* om de code op regel 40 te zien die de API aanroept met behulp van de gegenereerde client.</span><span class="sxs-lookup"><span data-stu-id="efe9a-307">In the ToDoListAPI project, open *Controllers\ToDoListController.cs* to see the code at line 40  that calls the API by using the generated client.</span></span>
   
    <span data-ttu-id="efe9a-308">Het volgende fragment toont hoe de code het clientobject instantieert en de Get-methode aanroept.</span><span class="sxs-lookup"><span data-stu-id="efe9a-308">The following snippet shows how the code instantiates the client object and calls the Get method.</span></span>
   
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
   
    <span data-ttu-id="efe9a-309">De constructorparameter haalt de eindpunt-URL uit de `toDoListDataAPIURL`-appinstelling.</span><span class="sxs-lookup"><span data-stu-id="efe9a-309">The constructor parameter gets the endpoint URL from  the `toDoListDataAPIURL` app setting.</span></span> <span data-ttu-id="efe9a-310">Deze waarde is in het bestand Web.config ingesteld op de lokale IIS Express URL van het API-project, zodat u de toepassing lokaal kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="efe9a-310">In the Web.config file, that value is set to the local IIS Express URL of the API project so that you can run the application locally.</span></span> <span data-ttu-id="efe9a-311">Als u de constructorparameter weglaat, wordt het standaardeindpunt de URL waaruit u de code hebt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-311">If you omit the constructor parameter, the default endpoint is the URL that you generated the code from.</span></span>
7. <span data-ttu-id="efe9a-312">De clientklasse wordt gegenereerd met een andere naam op basis van de naam van de API-app; wijzig de code in *Controllers\ToDoListController.cs*, zodat de typenaam overeenkomt met wat er in uw project is gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-312">Your client class will be generated with a different name based on your API app name; change the code in *Controllers\ToDoListController.cs* so that the type name matches what was generated in your project.</span></span> <span data-ttu-id="efe9a-313">Als de naam van uw API-app bijvoorbeeld ToDoListDataAPI071316 is, zou u deze code wijzigen:</span><span class="sxs-lookup"><span data-stu-id="efe9a-313">For example, if you named your API App ToDoListDataAPI071316, you would change this code:</span></span>
   
        private static ToDoListDataAPI NewDataAPIClient()
        {
            var client = new ToDoListDataAPI(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));

<span data-ttu-id="efe9a-314">in deze:</span><span class="sxs-lookup"><span data-stu-id="efe9a-314">to this:</span></span>

        private static ToDoListDataAPI071316 NewDataAPIClient()
        {
            var client = new ToDoListDataAPI071316(new Uri(ConfigurationManager.AppSettings["toDoListDataAPIURL"]));


## <a name="create-an-api-app-to-host-the-middle-tier"></a><span data-ttu-id="efe9a-315">Een API-app maken voor het hosten van de middelste laag</span><span class="sxs-lookup"><span data-stu-id="efe9a-315">Create an API app to host the middle tier</span></span>
<span data-ttu-id="efe9a-316">Eerder hebt u [de API-app voor de gegevenslaag gemaakt en er code in geïmplementeerd](#createapiapp).</span><span class="sxs-lookup"><span data-stu-id="efe9a-316">Earlier you [created the data tier API app and deployed code to it](#createapiapp).</span></span>  <span data-ttu-id="efe9a-317">Nu volgt u dezelfde procedure voor de API-app voor de middelste laag.</span><span class="sxs-lookup"><span data-stu-id="efe9a-317">Now you follow the same procedure for the middle tier API app.</span></span>

1. <span data-ttu-id="efe9a-318">Klik in **Solution Explorer** met de rechtermuisknop op het ToDoListAPI-project voor de middelste laag (niet op de ToDoListDataAPI voor de gegevenslaag) en klik vervolgens op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-318">In **Solution Explorer**, right-click the middle tier ToDoListAPI  project (not the data tier ToDoListDataAPI), and then click **Publish**.</span></span>
   
    ![Klikken op Publish in Visual Studio](./media/app-service-api-dotnet-get-started/pubinmenu2.png)
2. <span data-ttu-id="efe9a-320">Klik op het tabblad **Profile** van de wizard **Publish Web** op **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-320">In the **Profile** tab of the **Publish Web** wizard, click **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="efe9a-321">Klik in het dialoogvenster **App Service** op **New**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-321">In the **App Service** dialog box, click **New**.</span></span>
4. <span data-ttu-id="efe9a-322">Accepteer op het tabblad **Hosting** van het dialoogvenster **Create App Service** de standaardnaam bij **API App Name** of voer een andere naam in die uniek is in het domein *azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="efe9a-322">In the **Hosting** tab of the **Create App Service** dialog box, accept the default **API App Name** or enter a name that is unique in the *azurewebsites.net* domain.</span></span>
5. <span data-ttu-id="efe9a-323">Kies in **Subscription** het Azure-abonnement dat u momenteel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-323">Choose the Azure **Subscription** you have been using.</span></span>
6. <span data-ttu-id="efe9a-324">Kies in de vervolgkeuzelijst **Resource Group** dezelfde resourcegroep die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-324">In the **Resource Group** drop-down, choose the same resource group you created earlier.</span></span>
7. <span data-ttu-id="efe9a-325">Kies in de vervolgkeuzelijst **App Service Plan** hetzelfde abonnement dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-325">In the **App Service Plan** drop-down, choose the same plan you created earlier.</span></span> <span data-ttu-id="efe9a-326">Deze waarde wordt standaard ingesteld.</span><span class="sxs-lookup"><span data-stu-id="efe9a-326">It will default to that value.</span></span>
8. <span data-ttu-id="efe9a-327">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-327">Click **Create**.</span></span>
   
    <span data-ttu-id="efe9a-328">Visual Studio maakt de API-app, maakt er een publicatieprofiel voor en geeft de stap **Connection** van de wizard **Publish Web** weer.</span><span class="sxs-lookup"><span data-stu-id="efe9a-328">Visual Studio creates the API app, creates a publish profile for it, and displays the **Connection** step of the **Publish Web** wizard.</span></span>
9. <span data-ttu-id="efe9a-329">Klik in de stap **Connection** van de wizard **Publish Web** op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-329">In the **Connection** step of the **Publish Web** wizard, click **Publish**.</span></span>
   
   <span data-ttu-id="efe9a-330">Visual Studio implementeert het project TToDoListAPI in de nieuwe API-app en opent een browservenster met de URL van de API-app.</span><span class="sxs-lookup"><span data-stu-id="efe9a-330">Visual Studio deploys the ToDoListAPI project to the new API app and opens a browser to the URL of the API app.</span></span> <span data-ttu-id="efe9a-331">Er wordt een pagina weergegeven met de melding dat het maken is gelukt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-331">The "successfully created" page appears.</span></span>

## <a name="configure-the-middle-tier-to-call-the-data-tier"></a><span data-ttu-id="efe9a-332">De middelste laag configureren voor het aanroepen van de gegevenslaag</span><span class="sxs-lookup"><span data-stu-id="efe9a-332">Configure the middle tier to call the data tier</span></span>
<span data-ttu-id="efe9a-333">Als u de API-app voor de middelste laag nu aanroept, probeert deze de gegevenslaag aan te roepen via de localhost-URL die zich nog in het bestand Web.config bevindt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-333">If you called the middle tier API app now, it would try to call the data tier using the localhost URL that is still in the Web.config file.</span></span> <span data-ttu-id="efe9a-334">In deze sectie kunt u de API-app-URL voor de gegevenslaag invoeren in een omgevingsinstelling in de API-app voor de middelste laag.</span><span class="sxs-lookup"><span data-stu-id="efe9a-334">In this section you enter the data tier API app URL into an environment setting in the middle tier API app.</span></span> <span data-ttu-id="efe9a-335">Wanneer de code in de API-app voor de middelste laag de URL-instelling van de gegevenslaag ophaalt, overschrijft de omgevingsinstelling de inhoud van het bestand Web.config.</span><span class="sxs-lookup"><span data-stu-id="efe9a-335">When the code in the middle tier API app retrieves the data tier URL setting, the environment setting will override what's in the Web.config file.</span></span>

1. <span data-ttu-id="efe9a-336">Ga naar de [Azure Portal](https://portal.azure.com/) en navigeer naar de blade **API-app** van de API-app die u als host voor het project TodoListAPI (middelste laag) hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-336">Go to the [Azure portal](https://portal.azure.com/), and then navigate to the **API App** blade for the API app that you created to host the TodoListAPI (middle tier) project.</span></span>
2. <span data-ttu-id="efe9a-337">Klik op de blade **Instellingen** van de API-app op **Toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-337">In the API App's **Settings** blade, click **Application settings**.</span></span>
3. <span data-ttu-id="efe9a-338">Ga op de blade **Toepassingsinstellingen** van de API-app omlaag naar de sectie **App-instellingen** en voeg de volgende sleutel en waarde toe.</span><span class="sxs-lookup"><span data-stu-id="efe9a-338">In the API App's **Application Settings** blade, scroll down to the **App settings** section and add the following key and value.</span></span> <span data-ttu-id="efe9a-339">De waarde is de URL van de eerste API-app die u in deze zelfstudie hebt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="efe9a-339">The value will be the URL of the first API App you published in this tutorial.</span></span>
   
   | <span data-ttu-id="efe9a-340">**Sleutel**</span><span class="sxs-lookup"><span data-stu-id="efe9a-340">**Key**</span></span> | <span data-ttu-id="efe9a-341">toDoListDataAPIURL</span><span class="sxs-lookup"><span data-stu-id="efe9a-341">toDoListDataAPIURL</span></span> |
   | --- | --- |
   | <span data-ttu-id="efe9a-342">**Waarde**</span><span class="sxs-lookup"><span data-stu-id="efe9a-342">**Value**</span></span> |<span data-ttu-id="efe9a-343">https://{de naam van uw API-app voor de gegevenslaag}.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="efe9a-343">https://{your data tier API app name}.azurewebsites.net</span></span> |
   | <span data-ttu-id="efe9a-344">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="efe9a-344">**Example**</span></span> |<span data-ttu-id="efe9a-345">https://todolistdataapi.azurewebsites.net</span><span class="sxs-lookup"><span data-stu-id="efe9a-345">https://todolistdataapi.azurewebsites.net</span></span> |
4. <span data-ttu-id="efe9a-346">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="efe9a-346">Click **Save**.</span></span>
   
    ![Klikken op Opslaan in het gedeelte App-instellingen](./media/app-service-api-dotnet-get-started/asinportal.png)
   
    <span data-ttu-id="efe9a-348">Wanneer de code wordt uitgevoerd in Azure, overschrijft deze waarde de localhost-URL die zich in het Web.config-bestand bevindt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-348">When the code runs in Azure, this value will now override the localhost URL that is in the Web.config file.</span></span>

## <a name="test"></a><span data-ttu-id="efe9a-349">Testen</span><span class="sxs-lookup"><span data-stu-id="efe9a-349">Test</span></span>
1. <span data-ttu-id="efe9a-350">Open in een browservenster de URL van de nieuwe API-app voor de middelste laag die u zojuist hebt gemaakt voor ToDoListAPI.</span><span class="sxs-lookup"><span data-stu-id="efe9a-350">In a browser window, browse to the URL of the new middle tier API app that you just created for ToDoListAPI.</span></span> <span data-ttu-id="efe9a-351">Klik hiertoe op de URL op de hoofdblade van de API-app in de portal.</span><span class="sxs-lookup"><span data-stu-id="efe9a-351">You can get there by clicking the URL in the API app's main blade in the portal.</span></span>
2. <span data-ttu-id="efe9a-352">Voeg 'swagger' toe aan de URL in de adresbalk van de browser en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="efe9a-352">Add "swagger" to the URL in the browser's address bar, and then press Enter.</span></span> <span data-ttu-id="efe9a-353">(De URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span><span class="sxs-lookup"><span data-stu-id="efe9a-353">(The URL is `http://{apiappname}.azurewebsites.net/swagger`.)</span></span>
   
    <span data-ttu-id="efe9a-354">In de browser wordt dezelfde Swagger-gebruikersinterface weergegeven die u eerder hebt gezien voor ToDoListDataAPI. Nu is `owner` echter geen verplicht veld voor de Get-bewerking, omdat de API-app voor de middelste laag die waarde voor u naar de API-app voor de gegevenslaag verzendt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-354">The browser displays the same Swagger UI that you saw earlier for ToDoListDataAPI, but now `owner` is not a required field for the Get operation, because the middle tier API app is sending that value to the data tier API app for you.</span></span> <span data-ttu-id="efe9a-355">(Wanneer u de zelfstudies over verificatie volgt, verzendt de middelste laag werkelijke gebruikers-id’s voor de `owner`-parameter. In deze zelfstudie gebruiken we een hard gecodeerd sterretje.)</span><span class="sxs-lookup"><span data-stu-id="efe9a-355">(When you do the authentication tutorials, the middle tier will send actual user IDs for the `owner` parameter; for now it is hard-coding an asterisk.)</span></span>
3. <span data-ttu-id="efe9a-356">Probeer de Get-methode en de andere methoden om te valideren dat de API-app voor de middelste laag de API-app voor de gegevenslaag op correcte wijze aanroept.</span><span class="sxs-lookup"><span data-stu-id="efe9a-356">Try out the Get method and the other methods to validate that the middle tier API app is successfully calling the data tier API app.</span></span>
   
    ![Get-methode van de Swagger-gebruikersinterface](./media/app-service-api-dotnet-get-started/midtierget.png)

## <a name="troubleshooting"></a><span data-ttu-id="efe9a-358">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="efe9a-358">Troubleshooting</span></span>
<span data-ttu-id="efe9a-359">Als u tijdens het doorlopen van deze zelfstudie tegen problemen aanloopt, vindt u hier enkele ideeën voor probleemoplossing.</span><span class="sxs-lookup"><span data-stu-id="efe9a-359">In case you run into a problem as you go through this tutorial here are some troubleshooting ideas:</span></span>

* <span data-ttu-id="efe9a-360">Zorg ervoor dat u de nieuwste versie van de [Azure SDK voor .NET](http://go.microsoft.com/fwlink/?linkid=518003) gebruikt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-360">Make sure that you're using the latest version of the [Azure SDK for .NET](http://go.microsoft.com/fwlink/?linkid=518003).</span></span>
* <span data-ttu-id="efe9a-361">Twee van de projectnamen lijken erg op elkaar (ToDoListAPI, ToDoListDataAPI).</span><span class="sxs-lookup"><span data-stu-id="efe9a-361">Two of the project names are similar (ToDoListAPI, ToDoListDataAPI).</span></span> <span data-ttu-id="efe9a-362">Als dingen er tijdens het werken met een project niet zo uitzien als ze worden beschreven in de instructies, controleer dan of u het juiste project hebt geopend.</span><span class="sxs-lookup"><span data-stu-id="efe9a-362">If things don't look as described in the instructions when you are working with a project, make sure you have opened the correct project.</span></span>
* <span data-ttu-id="efe9a-363">Gebruikt u een bedrijfsnetwerk en probeert u Azure App Service via een firewall te implementeren, zorg er dan voor dat de poorten 443 en 8172 zijn geopend voor Web Deploy.</span><span class="sxs-lookup"><span data-stu-id="efe9a-363">If you're on a corporate network and are trying to deploy to Azure App Service through a firewall, make sure that ports 443 and 8172 are open for Web Deploy.</span></span> <span data-ttu-id="efe9a-364">Als u deze poorten niet kunt openen, gebruik dan een andere implementatiemethode.</span><span class="sxs-lookup"><span data-stu-id="efe9a-364">If you can't open those ports, you can use other deployment methods.</span></span>  <span data-ttu-id="efe9a-365">Zie [Een app implementeren in Azure App Service](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="efe9a-365">See [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md).</span></span>
* <span data-ttu-id="efe9a-366">Fouten van het type 'Routenamen moeten uniek zijn': mogelijk doen deze zich voor als u per ongeluk het verkeerde project in een API-app implementeert en vervolgens later het juiste project implementeert.</span><span class="sxs-lookup"><span data-stu-id="efe9a-366">"Route names must be unique" errors -- you could get these if you accidentally deploy the wrong project to an API app and then later deploy the correct one to it.</span></span> <span data-ttu-id="efe9a-367">U corrigeert dergelijke fouten door het juiste project opnieuw in de API-app te implementeren en op het tabblad **Settings** van de wizard **Publish Web** de optie **Remove additional files at destination** te selecteren.</span><span class="sxs-lookup"><span data-stu-id="efe9a-367">To correct this, redeploy the correct project to the API app, and on the **Settings** tab of the **Publish Web** wizard select **Remove additional files at destination**.</span></span>

<span data-ttu-id="efe9a-368">Wanneer uw ASP.NET-API-app eenmaal wordt uitgevoerd in Azure App Service, doet u er verstandig aan u te verdiepen in de Visual Studio-functies die het oplossen van problemen vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="efe9a-368">After you have your ASP.NET API app running in Azure App Service, you may want to learn more about Visual Studio features that simplify troubleshooting.</span></span> <span data-ttu-id="efe9a-369">Voor meer informatie over logboekregistratie, foutopsporing op afstand en meer raadpleegt u [Problemen met Azure App Service-apps in Visual Studio oplossen](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="efe9a-369">For information about logging, remote debugging, and more, see  [Troubleshooting Azure App Service apps in Visual Studio](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="efe9a-370">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="efe9a-370">Next steps</span></span>
<span data-ttu-id="efe9a-371">U hebt gezien hoe u bestaande Web API-projecten in API-apps kunt implementeren, clientcode kunt genereren voor API-apps en API-apps vanuit .NET-clients kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="efe9a-371">You've seen how to deploy existing Web API projects to API apps, generate client code for API apps, and consume API apps from .NET clients.</span></span> <span data-ttu-id="efe9a-372">In de volgende zelfstudie in deze reeks ziet u hoe u [CORS kunt toepassen om API-apps vanuit JavaScript-clients te gebruiken](app-service-api-cors-consume-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="efe9a-372">The next tutorial in this series shows how to [use CORS to consume API apps from JavaScript clients](app-service-api-cors-consume-javascript.md).</span></span>

<span data-ttu-id="efe9a-373">Zie de [Azure/AutoRest](https://github.com/azure/autorest)-opslagplaats op GitHub.com voor meer informatie over het genereren van clientcode.</span><span class="sxs-lookup"><span data-stu-id="efe9a-373">For more information about client code generation, see the [Azure/AutoRest](https://github.com/azure/autorest) repository on GitHub.com.</span></span> <span data-ttu-id="efe9a-374">Open een [actie-item in de AutoRest-opslagplaats](https://github.com/azure/autorest/issues) voor hulp bij problemen met het gebruik van de gegenereerde client.</span><span class="sxs-lookup"><span data-stu-id="efe9a-374">For help with problems using the generated client, open an [issue in the AutoRest repository](https://github.com/azure/autorest/issues).</span></span>

<span data-ttu-id="efe9a-375">Als u geheel nieuwe API-app-projecten wilt maken, gebruikt u de **Azure-API-app**-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="efe9a-375">If you want to create new API app projects from scratch, use the **Azure API App** template.</span></span>

![API-app-sjabloon in Visual Studio](./media/app-service-api-dotnet-get-started/apiapptemplate.png)

<span data-ttu-id="efe9a-377">Gebruik van de **Azure-API-app**-projectsjabloon geeft hetzelfde resultaat als wanneer u de **lege** ASP.NET 4.5.2-sjabloon kiest, het selectievakje inschakelt om Web API-ondersteuning toe te voegen en vervolgens het Swashbuckle NuGet-pakket installeert.</span><span class="sxs-lookup"><span data-stu-id="efe9a-377">The **Azure API App** project template is equivalent to choosing the **Empty** ASP.NET 4.5.2 template, clicking the check box to add Web API support, and installing the Swashbuckle NuGet package.</span></span> <span data-ttu-id="efe9a-378">Daarnaast voegt de sjabloon Swashbuckle-configuratiecode toe die tot doel heeft om te voorkomen dat er dubbele Swagger-bewerkings-id's worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="efe9a-378">In addition, the template adds some Swashbuckle configuration code designed to prevent the creation of duplicate Swagger operation IDs.</span></span> <span data-ttu-id="efe9a-379">Nadat u een API-app-project hebt gemaakt, kunt u dit op dezelfde manier implementeren in een API-app als u in deze zelfstudie hebt gezien.</span><span class="sxs-lookup"><span data-stu-id="efe9a-379">Once you've created an API App project, you can deploy it to an API app the same way you saw in this tutorial.</span></span>


---
title: aaaCustomize door Swashbuckle gegenereerde API-definities
description: Meer informatie over hoe toocustomize Swagger API-definities die worden gegenereerd door Swashbuckle voor een API-app in Azure App Service.
services: app-service\api
documentationcenter: .net
author: bradygaster
manager: erikre
editor: jimbe
ms.assetid: 6b8cbc38-d282-4a0f-b0c5-762631bae6f3
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: rachelap
ms.openlocfilehash: e31c665f8993533c5ec9a935e42cce34f86a5ade
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a><span data-ttu-id="fe988-103">Door Swashbuckle gegenereerde API-definities aanpassen</span><span class="sxs-lookup"><span data-stu-id="fe988-103">Customize Swashbuckle-generated API definitions</span></span>
## <a name="overview"></a><span data-ttu-id="fe988-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="fe988-104">Overview</span></span>
<span data-ttu-id="fe988-105">Dit artikel wordt uitgelegd hoe toocustomize Swashbuckle toohandle algemene scenario's waarin u tooalter kunt standaardgedrag Hallo:</span><span class="sxs-lookup"><span data-stu-id="fe988-105">This article explains how toocustomize Swashbuckle toohandle common scenarios where you may want tooalter hello default behavior:</span></span>

* <span data-ttu-id="fe988-106">Swashbuckle dubbele bewerkings-id's voor overloads van methoden van de domeincontroller genereert</span><span class="sxs-lookup"><span data-stu-id="fe988-106">Swashbuckle generates duplicate operation identifiers for overloads of controller methods</span></span>
* <span data-ttu-id="fe988-107">Swashbuckle wordt ervan uitgegaan dat Hallo alleen geldig antwoord van een methode HTTP 200 (OK is)</span><span class="sxs-lookup"><span data-stu-id="fe988-107">Swashbuckle assumes that hello only valid response from a method is HTTP 200 (OK)</span></span> 

## <a name="customize-operation-identifier-generation"></a><span data-ttu-id="fe988-108">Bewerking-ID generatie aanpassen</span><span class="sxs-lookup"><span data-stu-id="fe988-108">Customize operation identifier generation</span></span>
<span data-ttu-id="fe988-109">Swashbuckle genereert Swagger bewerking-id's door de naam van de domeincontroller en de methodenaam van de cookievalidatie.</span><span class="sxs-lookup"><span data-stu-id="fe988-109">Swashbuckle generates Swagger operation identifiers by concatenating controller name and method name.</span></span> <span data-ttu-id="fe988-110">Dit patroon maakt een probleem wanneer u meerdere overloads van een methode hebt: Swashbuckle dubbele bewerkings-id's, genereert, dit ongeldig Swagger JSON is.</span><span class="sxs-lookup"><span data-stu-id="fe988-110">This pattern creates a problem when you have multiple overloads of a method: Swashbuckle generates duplicate operation ids, which is invalid Swagger JSON.</span></span>

<span data-ttu-id="fe988-111">Bijvoorbeeld, Hallo na controllercode zorgt ervoor dat Swashbuckle toogenerate drie Contact_Get bewerking-id's.</span><span class="sxs-lookup"><span data-stu-id="fe988-111">For example, hello following controller code causes Swashbuckle toogenerate three Contact_Get operation ids.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

<span data-ttu-id="fe988-112">U kunt handmatig Hallo probleem oplossen door middel van een unieke namen, zoals de volgende Hallo voor dit voorbeeld Hallo methoden:</span><span class="sxs-lookup"><span data-stu-id="fe988-112">You can solve hello problem manually by giving hello methods unique names, such as hello following for this example:</span></span>

* <span data-ttu-id="fe988-113">Ophalen</span><span class="sxs-lookup"><span data-stu-id="fe988-113">Get</span></span>
* <span data-ttu-id="fe988-114">GetById</span><span class="sxs-lookup"><span data-stu-id="fe988-114">GetById</span></span>
* <span data-ttu-id="fe988-115">GetPage</span><span class="sxs-lookup"><span data-stu-id="fe988-115">GetPage</span></span>

<span data-ttu-id="fe988-116">Hallo alternatief is tooextend Swashbuckle toomake deze unieke bewerkings-id's voor het automatisch genereren.</span><span class="sxs-lookup"><span data-stu-id="fe988-116">hello alternative is tooextend Swashbuckle toomake it automatically generate unique operation ids.</span></span>

<span data-ttu-id="fe988-117">Hallo volgende stappen laten zien hoe toocustomize Swashbuckle met behulp van Hallo *SwaggerConfig.cs* -bestand dat is opgenomen in Hallo project door de projectsjabloon Hallo-Preview voor Visual Studio-API-Apps.</span><span class="sxs-lookup"><span data-stu-id="fe988-117">hello following steps show how toocustomize Swashbuckle by using hello *SwaggerConfig.cs* file that is included in hello project by hello Visual Studio API Apps Preview project template.</span></span>  <span data-ttu-id="fe988-118">U kunt ook Swashbuckle in een Web-API-project dat u voor implementatie als een API-app configureert aanpassen.</span><span class="sxs-lookup"><span data-stu-id="fe988-118">You can also customize Swashbuckle in a Web API project that you configure for deployment as an API app.</span></span>

1. <span data-ttu-id="fe988-119">Maak een aangepast `IOperationFilter` implementatie</span><span class="sxs-lookup"><span data-stu-id="fe988-119">Create a custom `IOperationFilter` implementation</span></span> 
   
    <span data-ttu-id="fe988-120">Hallo `IOperationFilter` interface biedt een uitbreidbaar punt voor Swashbuckle-gebruikers die toocustomize verschillende aspecten van Hallo Swagger-metagegevens proces.</span><span class="sxs-lookup"><span data-stu-id="fe988-120">hello `IOperationFilter` interface provides an extensibility point for Swashbuckle users who want toocustomize various aspects of hello Swagger metadata process.</span></span> <span data-ttu-id="fe988-121">Hallo toont volgende code een methode van het gedrag van de generatie-id-bewerking Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="fe988-121">hello following code demonstrates one method of changing hello operation-id-generation behavior.</span></span> <span data-ttu-id="fe988-122">Hallo-code worden namen toohello bewerking-id parameternaam toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="fe988-122">hello code appends parameter names toohello operation id name.</span></span>  
   
        using Swashbuckle.Swagger;
        using System.Web.Http.Description;
   
        namespace ContactsList
        {
            public class MultipleOperationsWithSameVerbFilter : IOperationFilter
            {
                public void Apply(
                    Operation operation,
                    SchemaRegistry schemaRegistry,
                    ApiDescription apiDescription)
                {
                    if (operation.parameters != null)
                    {
                        operation.operationId += "By";
                        foreach (var parm in operation.parameters)
                        {
                            operation.operationId += string.Format("{0}",parm.name);
                        }
                    }
                }
            }
        }
2. <span data-ttu-id="fe988-123">In *App_Start\SwaggerConfig.cs* bestand, aanroep Hallo `OperationFilter` methode toocause Swashbuckle toouse Hallo nieuwe `IOperationFilter` implementatie.</span><span class="sxs-lookup"><span data-stu-id="fe988-123">In *App_Start\SwaggerConfig.cs* file, call hello `OperationFilter` method toocause Swashbuckle toouse hello new `IOperationFilter` implementation.</span></span>
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    <span data-ttu-id="fe988-124">Hallo *SwaggerConfig.cs* -bestand dat is verwijderd door Hallo Swashbuckle NuGet-pakket bevat veel opmerkingen out voorbeelden van uitbreidbaarheidspunten.</span><span class="sxs-lookup"><span data-stu-id="fe988-124">hello *SwaggerConfig.cs* file that is dropped in by hello Swashbuckle NuGet package contains many commented-out examples of extensibility points.</span></span> <span data-ttu-id="fe988-125">Hallo aanvullende opmerkingen worden hier niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fe988-125">hello additional comments are not shown here.</span></span> 
   
    <span data-ttu-id="fe988-126">Nadat u deze wijziging aanbrengt uw `IOperationFilter` implementatie wordt gebruikt en zorgt ervoor dat unieke bewerkings-id's toobe gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="fe988-126">After you make this change, your `IOperationFilter` implementation is used and causes unique operation ids toobe generated.</span></span>
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a><span data-ttu-id="fe988-127">Reactiecodes dan 200 toestaan</span><span class="sxs-lookup"><span data-stu-id="fe988-127">Allow response codes other than 200</span></span>
<span data-ttu-id="fe988-128">Standaard Swashbuckle wordt ervan uitgegaan dat een HTTP 200 (OK) antwoord Hallo *alleen* rechtmatige reactie van een Web-API-methode.</span><span class="sxs-lookup"><span data-stu-id="fe988-128">By default, Swashbuckle assumes that an HTTP 200 (OK) response is hello *only* legitimate response from a Web API method.</span></span> <span data-ttu-id="fe988-129">In sommige gevallen kunt u tooreturn overige reactiecodes zonder Hallo client tooraise een uitzondering veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="fe988-129">In some cases, you may want tooreturn other response codes without causing hello client tooraise an exception.</span></span>  <span data-ttu-id="fe988-130">Bijvoorbeeld, hello volgende Web-API code toont een scenario waarin u Hallo client tooaccept zou willen een 200 of een 404 als geldige antwoorden.</span><span class="sxs-lookup"><span data-stu-id="fe988-130">For example, hello following Web API code demonstrates a scenario in which you would want hello client tooaccept either a 200 or a 404 as valid responses.</span></span>

    [ResponseType(typeof(Contact))]
    public HttpResponseMessage Get(int id)
    {
        var contacts = GetContacts();

        var requestedContact = contacts.FirstOrDefault(x => x.Id == id);

        if (requestedContact == null)
        {
            return Request.CreateResponse(HttpStatusCode.NotFound);
        }
        else
        {
            return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
        }
    }

<span data-ttu-id="fe988-131">In dit scenario bevat Hallo Swagger die Swashbuckle standaard genereert slechts één legitieme HTTP-statuscode HTTP 200.</span><span class="sxs-lookup"><span data-stu-id="fe988-131">In this scenario, hello Swagger that Swashbuckle generates by default specifies only one legitimate HTTP status code, HTTP 200.</span></span>

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

<span data-ttu-id="fe988-132">Omdat Hallo Swagger API-definitie toogenerate code Visual Studio voor de client hello gebruikt, maakt het clientcode die een uitzondering voor een antwoord dan een HTTP 200 genereert.</span><span class="sxs-lookup"><span data-stu-id="fe988-132">Since Visual Studio uses hello Swagger API definition toogenerate code for hello client, it creates client code that raises an exception for any response other than an HTTP 200.</span></span> <span data-ttu-id="fe988-133">Hallo-code hieronder is van een C#-client gegenereerd voor deze voorbeeld-Web-API-methode.</span><span class="sxs-lookup"><span data-stu-id="fe988-133">hello code below is from a C# client generated for this sample Web API method.</span></span>

    if (statusCode != HttpStatusCode.OK)
    {
        HttpOperationException<object> ex = new HttpOperationException<object>();
        ex.Request = httpRequest;
        ex.Response = httpResponse;
        ex.Body = null;
        if (shouldTrace)
        {
            ServiceClientTracing.Error(invocationId, ex);
        }
        throw ex;
    } 

<span data-ttu-id="fe988-134">Swashbuckle biedt twee manieren aan te passen Hallo-lijst van verwachte HTTP-antwoordcodes die wordt gegenereerd met XML-commentaar of Hallo `SwaggerResponse` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="fe988-134">Swashbuckle provides two ways of customizing hello list of expected HTTP response codes that it generates, using XML comments or hello `SwaggerResponse` attribute.</span></span> <span data-ttu-id="fe988-135">Hallo-kenmerk is gemakkelijker, maar is alleen beschikbaar in Swashbuckle 5.1.5 of hoger.</span><span class="sxs-lookup"><span data-stu-id="fe988-135">hello attribute is easier, but it is only available in Swashbuckle 5.1.5 or later.</span></span> <span data-ttu-id="fe988-136">Hallo API Apps preview nieuw project in Visual Studio 2013 bevat Swashbuckle versie 5.0.0, dus als u Hallo-sjabloon gebruikt en niet dat tooupdate Swashbuckle wilt, de enige optie toouse XML-commentaar.</span><span class="sxs-lookup"><span data-stu-id="fe988-136">hello API Apps preview new-project template in Visual Studio 2013 includes Swashbuckle version 5.0.0, so if you used hello template and don't want tooupdate Swashbuckle, your only option is toouse XML comments.</span></span> 

### <a name="customize-expected-response-codes-using-xml-comments"></a><span data-ttu-id="fe988-137">Verwachte reactiecodes met XML-commentaar aanpassen</span><span class="sxs-lookup"><span data-stu-id="fe988-137">Customize expected response codes using XML comments</span></span>
<span data-ttu-id="fe988-138">Gebruik deze methode toospecify antwoordcodes als uw Swashbuckle-versie ouder dan 5.1.5 is.</span><span class="sxs-lookup"><span data-stu-id="fe988-138">Use this method toospecify response codes if your Swashbuckle version is earlier than 5.1.5.</span></span>

1. <span data-ttu-id="fe988-139">Voeg eerst de XML-documentopmerkingen via Hallo-methoden die u wenst toospecify HTTP-antwoordcodes voor.</span><span class="sxs-lookup"><span data-stu-id="fe988-139">First, add XML documentation comments over hello methods you wish toospecify HTTP response codes for.</span></span> <span data-ttu-id="fe988-140">Verholpen Hallo voorbeeld-Web-API hierboven weergegeven en die van toepassing hello XML-documentatie tooit zou leiden tot code zoals Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="fe988-140">Taking hello sample Web API action shown above and applying hello XML documentation tooit would result in code like hello following example.</span></span> 
   
        /// <summary>
        /// Returns hello specified contact.
        /// </summary>
        /// <param name="id">hello ID of hello contact.</param>
        /// <returns>A contact record with an HTTP 200, or null with an HTTP 404.</returns>
        /// <response code="200">OK</response>
        /// <response code="404">Not Found</response>
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
   
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
2. <span data-ttu-id="fe988-141">Toevoegen van de instructies in Hallo *SwaggerConfig.cs* toodirect Swashbuckle toomake gebruik van de XML-documentatiebestand Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="fe988-141">Add instructions in hello *SwaggerConfig.cs* file toodirect Swashbuckle toomake use of hello XML documentation file.</span></span>
   
   * <span data-ttu-id="fe988-142">Open *SwaggerConfig.cs* en maakt u een methode op Hallo *SwaggerConfig* klasse toospecify Hallo pad toohello XML-documentatiebestand.</span><span class="sxs-lookup"><span data-stu-id="fe988-142">Open *SwaggerConfig.cs* and create a method on hello *SwaggerConfig* class toospecify hello path toohello documentation XML file.</span></span> 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * <span data-ttu-id="fe988-143">Schuif omlaag in Hallo *SwaggerConfig.cs* totdat er Hallo opmerkingen out coderegel die lijkt op de onderstaande schermafdruk Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="fe988-143">Scroll down in hello *SwaggerConfig.cs* file until you see hello commented-out line of code resembling hello screen shot below.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * <span data-ttu-id="fe988-144">Verwijder de opmerkingen in Hallo regel tooenable Hallo XML-commentaar verwerking tijdens het genereren van Swagger.</span><span class="sxs-lookup"><span data-stu-id="fe988-144">Uncomment hello line tooenable hello XML comments processing during Swagger generation.</span></span> 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. <span data-ttu-id="fe988-145">Ga naar eigenschappen van het project Hallo in volgorde toogenerate Hallo XML-documentatiebestand, en Hallo XML-documentatiebestand zoals weergegeven in onderstaande schermafbeelding voor Hallo inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fe988-145">In order toogenerate hello XML documentation file, go into hello project's properties and enable hello XML documentation file as shown in hello screenshot below.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

<span data-ttu-id="fe988-146">Nadat u deze stappen hebt uitgevoerd, bevatten Hallo Swagger JSON die worden gegenereerd door Swashbuckle Hallo HTTP-antwoordcodes die u hebt opgegeven in Hallo XML-opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="fe988-146">Once you perform these steps, hello Swagger JSON generated by Swashbuckle will reflect hello HTTP response codes that you specified in hello XML comments.</span></span> <span data-ttu-id="fe988-147">Hallo onderstaande schermafbeelding ziet u deze nieuwe JSON-nettolading.</span><span class="sxs-lookup"><span data-stu-id="fe988-147">hello screenshot below demonstrates this new JSON payload.</span></span> 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

<span data-ttu-id="fe988-148">Wanneer u Visual Studio tooregenerate Hallo clientcode voor uw REST API, accepteert Hallo C#-code beide statuscodes Hallo HTTP OK en niet gevonden zonder een uitzondering, zodat uw consumerende code toomake beslissingen op hoe toohandle Hallo retourneren van een null-waarde Neem contact op met een record.</span><span class="sxs-lookup"><span data-stu-id="fe988-148">When you use Visual Studio tooregenerate hello client code for your REST API, hello C# code accepts both hello HTTP OK and Not Found status codes without raising an exception, allowing your consuming code toomake decisions on how toohandle hello return of a null Contact record.</span></span> 

        if (statusCode != HttpStatusCode.OK && statusCode != HttpStatusCode.NotFound)
        {
            HttpOperationException<object> ex = new HttpOperationException<object>();
            ex.Request = httpRequest;
            ex.Response = httpResponse;
            ex.Body = null;
            if (shouldTrace)
            {
                ServiceClientTracing.Error(invocationId, ex);
            }
                throw ex;
        }

<span data-ttu-id="fe988-149">Hallo-code voor deze demonstratie kunt u vinden in [deze GitHub-opslagplaats](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span><span class="sxs-lookup"><span data-stu-id="fe988-149">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse).</span></span> <span data-ttu-id="fe988-150">Samen met de Hallo Web-API is gemarkeerd met XML-documentopmerkingen project een consoletoepassingsproject die een gegenereerde client voor deze API bevat.</span><span class="sxs-lookup"><span data-stu-id="fe988-150">Along with hello Web API project marked up with XML documentation comments is a Console Application project that contains a generated client for this API.</span></span> 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a><span data-ttu-id="fe988-151">Verwachte reactiecodes met Hallo SwaggerResponse kenmerk aanpassen</span><span class="sxs-lookup"><span data-stu-id="fe988-151">Customize expected response codes using hello SwaggerResponse attribute</span></span>
<span data-ttu-id="fe988-152">Hallo [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) kenmerk is beschikbaar in Swashbuckle 5.1.5 en hoger.</span><span class="sxs-lookup"><span data-stu-id="fe988-152">hello [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) attribute is available in Swashbuckle 5.1.5 and later.</span></span> <span data-ttu-id="fe988-153">Als u een eerdere versie in uw project hebt, wordt in deze sectie begint met het waarin wordt uitgelegd hoe tooupdate hello Swashbuckle NuGet-pakket zodat u kunt dit kenmerk.</span><span class="sxs-lookup"><span data-stu-id="fe988-153">In case you have an earlier version in your project, this section starts by explaining how tooupdate hello Swashbuckle NuGet package so that you can use this attribute.</span></span>

1. <span data-ttu-id="fe988-154">In **Solution Explorer**, met de rechtermuisknop op uw Web API-project en klik op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="fe988-154">In **Solution Explorer**, right-click your Web API project and click **Manage NuGet Packages**.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. <span data-ttu-id="fe988-155">Klik op Hallo *Update* knop volgende toohello *Swashbuckle* NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="fe988-155">Click hello *Update* button next toohello *Swashbuckle* NuGet package.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. <span data-ttu-id="fe988-156">Hallo toevoegen *SwaggerResponse* toohello Web API-actiemethoden waarvoor u toospecify geldig HTTP-antwoordcodes wilt kenmerken.</span><span class="sxs-lookup"><span data-stu-id="fe988-156">Add hello *SwaggerResponse* attributes toohello Web API action methods for which you want toospecify valid HTTP response codes.</span></span> 
   
        [SwaggerResponse(HttpStatusCode.OK)]
        [SwaggerResponse(HttpStatusCode.NotFound)]
        [ResponseType(typeof(Contact))]
        public HttpResponseMessage Get(int id)
        {
            var contacts = GetContacts();
   
            var requestedContact = contacts.FirstOrDefault(x => x.Id == id);
            if (requestedContact == null)
            {
                return Request.CreateResponse(HttpStatusCode.NotFound);
            }
            else
            {
                return Request.CreateResponse<Contact>(HttpStatusCode.OK, requestedContact);
            }
        }
4. <span data-ttu-id="fe988-157">Voeg een `using` -instructie voor het Hallo-kenmerk namespace:</span><span class="sxs-lookup"><span data-stu-id="fe988-157">Add a `using` statement for hello attribute's namespace:</span></span>
   
        using Swashbuckle.Swagger.Annotations;
5. <span data-ttu-id="fe988-158">Blader toohello */swagger/docs/v1* URL van uw project en verschillende HTTP-antwoordcodes zijn zichtbaar in Hallo Hallo Swagger JSON.</span><span class="sxs-lookup"><span data-stu-id="fe988-158">Browse toohello */swagger/docs/v1* URL of your project and hello various HTTP response codes will be visible in hello Swagger JSON.</span></span> 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

<span data-ttu-id="fe988-159">Hallo-code voor deze demonstratie kunt u vinden in [deze GitHub-opslagplaats](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span><span class="sxs-lookup"><span data-stu-id="fe988-159">hello code for this demonstration can be found in [this GitHub repository](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes).</span></span> <span data-ttu-id="fe988-160">Samen met de Hallo Web API-project gedecoreerd worden met Hallo *SwaggerResponse* kenmerk is een consoletoepassingsproject die een gegenereerde client voor deze API bevat.</span><span class="sxs-lookup"><span data-stu-id="fe988-160">Along with hello Web API project decorated with hello *SwaggerResponse* attribute is a Console Application project that contains a generated client for this API.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fe988-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fe988-161">Next steps</span></span>
<span data-ttu-id="fe988-162">In dit artikel heeft geleerd hoe toocustomize Hallo manier Swashbuckle bewerking-id's en geldig reactiecodes genereert.</span><span class="sxs-lookup"><span data-stu-id="fe988-162">This article has shown how toocustomize hello way Swashbuckle generates operation ids and valid response codes.</span></span> <span data-ttu-id="fe988-163">Zie voor meer informatie [Swashbuckle op GitHub](https://github.com/domaindrivendev/Swashbuckle).</span><span class="sxs-lookup"><span data-stu-id="fe988-163">For more information, see [Swashbuckle on GitHub](https://github.com/domaindrivendev/Swashbuckle).</span></span>


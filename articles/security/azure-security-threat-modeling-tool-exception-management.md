---
title: aaaException Azure Management - Microsoft Threat Modeling Tool - | Microsoft Docs
description: oplossingen voor bedreigingen die worden weergegeven in Hallo Threat Modeling hulpprogramma
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 247096c10deeca94ebb9b19df7ba60e442ca1e4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-exception-management--mitigations"></a><span data-ttu-id="5b285-103">Beveiliging Frame: Uitzonderingsbeheer | Oplossingen</span><span class="sxs-lookup"><span data-stu-id="5b285-103">Security Frame: Exception Management | Mitigations</span></span> 
| <span data-ttu-id="5b285-104">Product/Service</span><span class="sxs-lookup"><span data-stu-id="5b285-104">Product/Service</span></span> | <span data-ttu-id="5b285-105">Artikel</span><span class="sxs-lookup"><span data-stu-id="5b285-105">Article</span></span> |
| --------------- | ------- |
| <span data-ttu-id="5b285-106">**WCF**</span><span class="sxs-lookup"><span data-stu-id="5b285-106">**WCF**</span></span> | <ul><li>[<span data-ttu-id="5b285-107">WCF - Do serviceDebug knooppunt niet opgenomen in het configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="5b285-107">WCF- Do not include serviceDebug node in configuration file</span></span>](#servicedebug)</li><li>[<span data-ttu-id="5b285-108">WCF - Do serviceMetadata knooppunt niet opgenomen in het configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="5b285-108">WCF- Do not include serviceMetadata node in configuration file</span></span>](#servicemetadata)</li></ul> |
| <span data-ttu-id="5b285-109">**Web-API**</span><span class="sxs-lookup"><span data-stu-id="5b285-109">**Web API**</span></span> | <ul><li>[<span data-ttu-id="5b285-110">Zorg ervoor dat de juiste uitzonderingsverwerking in ASP.NET Web API is uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="5b285-110">Ensure that proper exception handling is done in ASP.NET Web API </span></span>](#exception)</li></ul> |
| <span data-ttu-id="5b285-111">**Webtoepassing**</span><span class="sxs-lookup"><span data-stu-id="5b285-111">**Web Application**</span></span> | <ul><li>[<span data-ttu-id="5b285-112">Informatie over de beveiliging in foutberichten niet zichtbaar</span><span class="sxs-lookup"><span data-stu-id="5b285-112">Do not expose security details in error messages </span></span>](#messages)</li><li>[<span data-ttu-id="5b285-113">Standaard-fout tijdens het verwerken van pagina implementeren</span><span class="sxs-lookup"><span data-stu-id="5b285-113">Implement Default error handling page </span></span>](#default)</li><li>[<span data-ttu-id="5b285-114">Implementatiemethode tooRetail instellen in IIS</span><span class="sxs-lookup"><span data-stu-id="5b285-114">Set Deployment Method tooRetail in IIS</span></span>](#deployment)</li><li>[<span data-ttu-id="5b285-115">Uitzonderingen zou moeten veilig mislukken</span><span class="sxs-lookup"><span data-stu-id="5b285-115">Exceptions should fail safely</span></span>](#fail)</li></ul> |

## <span data-ttu-id="5b285-116"><a id="servicedebug"></a>WCF - Do serviceDebug knooppunt niet opgenomen in het configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="5b285-116"><a id="servicedebug"></a>WCF- Do not include serviceDebug node in configuration file</span></span>

| <span data-ttu-id="5b285-117">Titel</span><span class="sxs-lookup"><span data-stu-id="5b285-117">Title</span></span>                   | <span data-ttu-id="5b285-118">Details</span><span class="sxs-lookup"><span data-stu-id="5b285-118">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b285-119">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="5b285-119">**Component**</span></span>               | <span data-ttu-id="5b285-120">WCF</span><span class="sxs-lookup"><span data-stu-id="5b285-120">WCF</span></span> | 
| <span data-ttu-id="5b285-121">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="5b285-121">**SDL Phase**</span></span>               | <span data-ttu-id="5b285-122">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="5b285-122">Build</span></span> |  
| <span data-ttu-id="5b285-123">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="5b285-123">**Applicable Technologies**</span></span> | <span data-ttu-id="5b285-124">Algemeen, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="5b285-124">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="5b285-125">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="5b285-125">**Attributes**</span></span>              | <span data-ttu-id="5b285-126">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="5b285-126">N/A</span></span>  |
| <span data-ttu-id="5b285-127">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="5b285-127">**References**</span></span>              | <span data-ttu-id="5b285-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg Koninkrijk](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="5b285-128">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="5b285-129">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="5b285-129">**Steps**</span></span> | <span data-ttu-id="5b285-130">Framework WCF (Windows Communication) services kunnen de geconfigureerde tooexpose foutopsporingsgegevens zijn.</span><span class="sxs-lookup"><span data-stu-id="5b285-130">Windows Communication Framework (WCF) services can be configured tooexpose debugging information.</span></span> <span data-ttu-id="5b285-131">Fouten opsporen informatie mag niet worden gebruikt in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="5b285-131">Debug information should not be used in production environments.</span></span> <span data-ttu-id="5b285-132">Hallo `<serviceDebug>` tag definieert of functie Hallo debug-gegevens voor een WCF-service is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5b285-132">hello `<serviceDebug>` tag defines whether hello debug information feature is enabled for a WCF service.</span></span> <span data-ttu-id="5b285-133">Als Hallo kenmerk includeExceptionDetailInFaults is tootrue ingesteld, wordt uitzonderingsinformatie van de toepassing hello tooclients worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5b285-133">If hello attribute includeExceptionDetailInFaults is set tootrue, exception information from hello application will be returned tooclients.</span></span> <span data-ttu-id="5b285-134">Aanvallers kunnen gebruikmaken van Hallo aanvullende informatie ze krijgen uit de uitvoer toomount aanvallen gericht op Hallo framework, database of andere resources gebruikt door de toepassing hello foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="5b285-134">Attackers can leverage hello additional information they gain from debugging output toomount attacks targeted on hello framework, database, or other resources used by hello application.</span></span> |

### <a name="example"></a><span data-ttu-id="5b285-135">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5b285-135">Example</span></span>
<span data-ttu-id="5b285-136">Hallo volgende configuratiebestand bevat Hallo `<serviceDebug>` tag:</span><span class="sxs-lookup"><span data-stu-id="5b285-136">hello following configuration file includes hello `<serviceDebug>` tag:</span></span> 
```
<configuration> 
<system.serviceModel> 
<behaviors> 
<serviceBehaviors> 
<behavior name=""MyServiceBehavior""> 
<serviceDebug includeExceptionDetailInFaults=""True"" httpHelpPageEnabled=""True""/> 
... 
```
<span data-ttu-id="5b285-137">Informatie voor foutopsporing in Hallo service uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="5b285-137">Disable debugging information in hello service.</span></span> <span data-ttu-id="5b285-138">Kan dit worden bereikt door het verwijderen van Hallo `<serviceDebug>` tag uit het configuratiebestand van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5b285-138">This can be accomplished by removing hello `<serviceDebug>` tag from your application's configuration file.</span></span> 

## <span data-ttu-id="5b285-139"><a id="servicemetadata"></a>WCF - Do serviceMetadata knooppunt niet opgenomen in het configuratiebestand</span><span class="sxs-lookup"><span data-stu-id="5b285-139"><a id="servicemetadata"></a>WCF- Do not include serviceMetadata node in configuration file</span></span>

| <span data-ttu-id="5b285-140">Titel</span><span class="sxs-lookup"><span data-stu-id="5b285-140">Title</span></span>                   | <span data-ttu-id="5b285-141">Details</span><span class="sxs-lookup"><span data-stu-id="5b285-141">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b285-142">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="5b285-142">**Component**</span></span>               | <span data-ttu-id="5b285-143">WCF</span><span class="sxs-lookup"><span data-stu-id="5b285-143">WCF</span></span> | 
| <span data-ttu-id="5b285-144">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="5b285-144">**SDL Phase**</span></span>               | <span data-ttu-id="5b285-145">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="5b285-145">Build</span></span> |  
| <span data-ttu-id="5b285-146">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="5b285-146">**Applicable Technologies**</span></span> | <span data-ttu-id="5b285-147">Algemene</span><span class="sxs-lookup"><span data-stu-id="5b285-147">Generic</span></span> |
| <span data-ttu-id="5b285-148">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="5b285-148">**Attributes**</span></span>              | <span data-ttu-id="5b285-149">Algemeen, NET Framework 3</span><span class="sxs-lookup"><span data-stu-id="5b285-149">Generic, NET Framework 3</span></span> |
| <span data-ttu-id="5b285-150">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="5b285-150">**References**</span></span>              | <span data-ttu-id="5b285-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Voeg Koninkrijk](https://vulncat.fortify.com/en/vulncat/index.html)</span><span class="sxs-lookup"><span data-stu-id="5b285-151">[MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html)</span></span> |
| <span data-ttu-id="5b285-152">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="5b285-152">**Steps**</span></span> | <span data-ttu-id="5b285-153">Informatie over een service openbaar vrijgeeft, kan aanvallers waardevolle inzicht in hoe ze Hallo-service kunnen misbruiken bieden.</span><span class="sxs-lookup"><span data-stu-id="5b285-153">Publicly exposing information about a service can provide attackers with valuable insight into how they might exploit hello service.</span></span> <span data-ttu-id="5b285-154">Hallo `<serviceMetadata>` code kan publicatiefunctie Hallo-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="5b285-154">hello `<serviceMetadata>` tag enables hello metadata publishing feature.</span></span> <span data-ttu-id="5b285-155">Metagegevens van de service kan gevoelige gegevens bevatten die niet moet openbaar toegankelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="5b285-155">Service metadata could contain sensitive information that should not be publicly accessible.</span></span> <span data-ttu-id="5b285-156">Ten minste staan alleen vertrouwde gebruikers tooaccess Hallo metagegevens en zorg ervoor dat onnodige informatie is niet beschikbaar gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5b285-156">At a minimum, only allow trusted users tooaccess hello metadata and ensure that unnecessary information is not exposed.</span></span> <span data-ttu-id="5b285-157">Volledig uitschakelen nog beter Hallo mogelijkheid toopublish metagegevens.</span><span class="sxs-lookup"><span data-stu-id="5b285-157">Better yet, entirely disable hello ability toopublish metadata.</span></span> <span data-ttu-id="5b285-158">Een veilige WCF-configuratie bevat geen Hallo `<serviceMetadata>` label.</span><span class="sxs-lookup"><span data-stu-id="5b285-158">A safe WCF configuration will not contain hello `<serviceMetadata>` tag.</span></span> |

## <span data-ttu-id="5b285-159"><a id="exception"></a>Zorg ervoor dat de juiste uitzonderingsverwerking in ASP.NET Web API is uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="5b285-159"><a id="exception"></a>Ensure that proper exception handling is done in ASP.NET Web API</span></span>

| <span data-ttu-id="5b285-160">Titel</span><span class="sxs-lookup"><span data-stu-id="5b285-160">Title</span></span>                   | <span data-ttu-id="5b285-161">Details</span><span class="sxs-lookup"><span data-stu-id="5b285-161">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b285-162">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="5b285-162">**Component**</span></span>               | <span data-ttu-id="5b285-163">Web-API</span><span class="sxs-lookup"><span data-stu-id="5b285-163">Web API</span></span> | 
| <span data-ttu-id="5b285-164">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="5b285-164">**SDL Phase**</span></span>               | <span data-ttu-id="5b285-165">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="5b285-165">Build</span></span> |  
| <span data-ttu-id="5b285-166">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="5b285-166">**Applicable Technologies**</span></span> | <span data-ttu-id="5b285-167">MVC 5, 6 MVC</span><span class="sxs-lookup"><span data-stu-id="5b285-167">MVC 5, MVC 6</span></span> |
| <span data-ttu-id="5b285-168">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="5b285-168">**Attributes**</span></span>              | <span data-ttu-id="5b285-169">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="5b285-169">N/A</span></span>  |
| <span data-ttu-id="5b285-170">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="5b285-170">**References**</span></span>              | <span data-ttu-id="5b285-171">[Afhandeling van uitzonderingen in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model validatie in ASP.NET-Web-API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span><span class="sxs-lookup"><span data-stu-id="5b285-171">[Exception Handling in ASP.NET Web API](http://www.asp.net/web-api/overview/error-handling/exception-handling), [Model Validation in ASP.NET Web API](http://www.asp.net/web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api)</span></span> |
| <span data-ttu-id="5b285-172">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="5b285-172">**Steps**</span></span> | <span data-ttu-id="5b285-173">Standaard worden meest niet-onderschepte uitzonderingen in ASP.NET Web API vertaald in een HTTP-antwoord met de statuscode`500, Internal Server Error`</span><span class="sxs-lookup"><span data-stu-id="5b285-173">By default, most uncaught exceptions in ASP.NET Web API are translated into an HTTP response with status code `500, Internal Server Error`</span></span>|

### <a name="example"></a><span data-ttu-id="5b285-174">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5b285-174">Example</span></span>
<span data-ttu-id="5b285-175">toocontrol Hallo-statuscode geretourneerd door Hallo API, `HttpResponseException` kan worden gebruikt, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5b285-175">toocontrol hello status code returned by hello API, `HttpResponseException` can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}
```

### <a name="example"></a><span data-ttu-id="5b285-176">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5b285-176">Example</span></span>
<span data-ttu-id="5b285-177">Voor verdere besturingselement in het antwoord van de uitzondering Hallo Hallo `HttpResponseMessage` klasse kan worden gebruikt, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5b285-177">For further control on hello exception response, hello `HttpResponseMessage` class can be used as shown below:</span></span> 
```C#
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        }
        throw new HttpResponseException(resp);
    }
    return item;
}
```
<span data-ttu-id="5b285-178">toocatch onverwerkte uitzonderingen die niet van het type Hallo `HttpResponseException`, uitzondering Filters kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5b285-178">toocatch unhandled exceptions that are not of hello type `HttpResponseException`, Exception Filters can be used.</span></span> <span data-ttu-id="5b285-179">Uitzondering filters implementeren Hallo `System.Web.Http.Filters.IExceptionFilter` interface.</span><span class="sxs-lookup"><span data-stu-id="5b285-179">Exception filters implement hello `System.Web.Http.Filters.IExceptionFilter` interface.</span></span> <span data-ttu-id="5b285-180">Hallo eenvoudigste manier toowrite een uitzonderingsfilter wordt tooderive van Hallo `System.Web.Http.Filters.ExceptionFilterAttribute` klasse en Hallo OnException methode overschrijven.</span><span class="sxs-lookup"><span data-stu-id="5b285-180">hello simplest way toowrite an exception filter is tooderive from hello `System.Web.Http.Filters.ExceptionFilterAttribute` class and override hello OnException method.</span></span> 

### <a name="example"></a><span data-ttu-id="5b285-181">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5b285-181">Example</span></span>
<span data-ttu-id="5b285-182">Hier volgt een filter dat wordt geconverteerd `NotImplementedException` uitzonderingen in de HTTP-statuscode `501, Not Implemented`:</span><span class="sxs-lookup"><span data-stu-id="5b285-182">Here is a filter that converts `NotImplementedException` exceptions into HTTP status code `501, Not Implemented`:</span></span> 
```C#
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```

<span data-ttu-id="5b285-183">Er zijn verschillende manieren tooregister een uitzonderingsfilter Web-API:</span><span class="sxs-lookup"><span data-stu-id="5b285-183">There are several ways tooregister a Web API exception filter:</span></span>
- <span data-ttu-id="5b285-184">Door de actie</span><span class="sxs-lookup"><span data-stu-id="5b285-184">By action</span></span>
- <span data-ttu-id="5b285-185">Door de netwerkcontroller</span><span class="sxs-lookup"><span data-stu-id="5b285-185">By controller</span></span>
- <span data-ttu-id="5b285-186">Globaal</span><span class="sxs-lookup"><span data-stu-id="5b285-186">Globally</span></span>

### <a name="example"></a><span data-ttu-id="5b285-187">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5b285-187">Example</span></span>
<span data-ttu-id="5b285-188">tooapply hello tooa specifieke actie filteren, Hallo-filter toevoegen als een kenmerk toohello actie:</span><span class="sxs-lookup"><span data-stu-id="5b285-188">tooapply hello filter tooa specific action, add hello filter as an attribute toohello action:</span></span> 
```C#
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
### <a name="example"></a><span data-ttu-id="5b285-189">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5b285-189">Example</span></span>
<span data-ttu-id="5b285-190">tooapply hello filter tooall Hallo acties op een `controller`, Hallo-filter toevoegen als een kenmerk toohello `controller` klasse:</span><span class="sxs-lookup"><span data-stu-id="5b285-190">tooapply hello filter tooall of hello actions on a `controller`, add hello filter as an attribute toohello `controller` class:</span></span> 

```C#
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```

### <a name="example"></a><span data-ttu-id="5b285-191">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5b285-191">Example</span></span>
<span data-ttu-id="5b285-192">tooapply Hallo filteren globaal tooall Web API-controllers, Voeg een exemplaar van Hallo filter toohello `GlobalConfiguration.Configuration.Filters` verzameling.</span><span class="sxs-lookup"><span data-stu-id="5b285-192">tooapply hello filter globally tooall Web API controllers, add an instance of hello filter toohello `GlobalConfiguration.Configuration.Filters` collection.</span></span> <span data-ttu-id="5b285-193">Uitzondering filters in deze verzameling toepassen tooany Web API-controller actie.</span><span class="sxs-lookup"><span data-stu-id="5b285-193">Exception filters in this collection apply tooany Web API controller action.</span></span> 
```C#
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

### <a name="example"></a><span data-ttu-id="5b285-194">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5b285-194">Example</span></span>
<span data-ttu-id="5b285-195">Voor de validatie, kan de Hallo modelstatus worden doorgegeven aan tooCreateErrorResponse methode, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5b285-195">For model validation, hello model state can be passed tooCreateErrorResponse method as shown below:</span></span> 
```C#
public HttpResponseMessage PostProduct(Product item)
{
    if (!ModelState.IsValid)
    {
        return Request.CreateErrorResponse(HttpStatusCode.BadRequest, ModelState);
    }
    // Implementation not shown...
}
```

<span data-ttu-id="5b285-196">Hallo-koppelingen in Hallo verwijzingen gedeelte voor meer informatie over het afhandelen van uitzonderlijke en modelvalidatie van het in ASP.Net Web API controleren</span><span class="sxs-lookup"><span data-stu-id="5b285-196">Check hello links in hello references section for additional details about exceptional handling and model validation in ASP.Net Web API</span></span> 

## <span data-ttu-id="5b285-197"><a id="messages"></a>Informatie over de beveiliging in foutberichten niet zichtbaar</span><span class="sxs-lookup"><span data-stu-id="5b285-197"><a id="messages"></a>Do not expose security details in error messages</span></span>

| <span data-ttu-id="5b285-198">Titel</span><span class="sxs-lookup"><span data-stu-id="5b285-198">Title</span></span>                   | <span data-ttu-id="5b285-199">Details</span><span class="sxs-lookup"><span data-stu-id="5b285-199">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b285-200">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="5b285-200">**Component**</span></span>               | <span data-ttu-id="5b285-201">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="5b285-201">Web Application</span></span> | 
| <span data-ttu-id="5b285-202">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="5b285-202">**SDL Phase**</span></span>               | <span data-ttu-id="5b285-203">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="5b285-203">Build</span></span> |  
| <span data-ttu-id="5b285-204">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="5b285-204">**Applicable Technologies**</span></span> | <span data-ttu-id="5b285-205">Algemene</span><span class="sxs-lookup"><span data-stu-id="5b285-205">Generic</span></span> |
| <span data-ttu-id="5b285-206">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="5b285-206">**Attributes**</span></span>              | <span data-ttu-id="5b285-207">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="5b285-207">N/A</span></span>  |
| <span data-ttu-id="5b285-208">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="5b285-208">**References**</span></span>              | <span data-ttu-id="5b285-209">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="5b285-209">N/A</span></span>  |
| <span data-ttu-id="5b285-210">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="5b285-210">**Steps**</span></span> | <p><span data-ttu-id="5b285-211">Algemene foutberichten worden verstrekt rechtstreeks toohello gebruiker zonder met inbegrip van gegevens voor gevoelige toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5b285-211">Generic error messages are provided directly toohello user without including sensitive application data.</span></span> <span data-ttu-id="5b285-212">Voorbeelden van gevoelige gegevens omvatten:</span><span class="sxs-lookup"><span data-stu-id="5b285-212">Examples of sensitive data include:</span></span></p><ul><li><span data-ttu-id="5b285-213">Namen van server</span><span class="sxs-lookup"><span data-stu-id="5b285-213">Server names</span></span></li><li><span data-ttu-id="5b285-214">Verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="5b285-214">Connection strings</span></span></li><li><span data-ttu-id="5b285-215">Gebruikersnamen</span><span class="sxs-lookup"><span data-stu-id="5b285-215">Usernames</span></span></li><li><span data-ttu-id="5b285-216">Wachtwoorden</span><span class="sxs-lookup"><span data-stu-id="5b285-216">Passwords</span></span></li><li><span data-ttu-id="5b285-217">SQL-procedures</span><span class="sxs-lookup"><span data-stu-id="5b285-217">SQL procedures</span></span></li><li><span data-ttu-id="5b285-218">Details van dynamische SQL-fouten</span><span class="sxs-lookup"><span data-stu-id="5b285-218">Details of dynamic SQL failures</span></span></li><li><span data-ttu-id="5b285-219">Stack-trace en de regels van code</span><span class="sxs-lookup"><span data-stu-id="5b285-219">Stack trace and lines of code</span></span></li><li><span data-ttu-id="5b285-220">Variabelen die zijn opgeslagen in het geheugen</span><span class="sxs-lookup"><span data-stu-id="5b285-220">Variables stored in memory</span></span></li><li><span data-ttu-id="5b285-221">Station en de map locaties</span><span class="sxs-lookup"><span data-stu-id="5b285-221">Drive and folder locations</span></span></li><li><span data-ttu-id="5b285-222">Toepassing installeren punten</span><span class="sxs-lookup"><span data-stu-id="5b285-222">Application install points</span></span></li><li><span data-ttu-id="5b285-223">Host-configuratie-instellingen</span><span class="sxs-lookup"><span data-stu-id="5b285-223">Host configuration settings</span></span></li><li><span data-ttu-id="5b285-224">Andere details interne toepassing</span><span class="sxs-lookup"><span data-stu-id="5b285-224">Other internal application details</span></span></li></ul><p><span data-ttu-id="5b285-225">Alle fouten in een toepassing onderscheppen en algemene foutberichten bieden, evenals aangepaste fouten in IIS inschakelen wordt voorkomen dat openbaarmaking van informatie.</span><span class="sxs-lookup"><span data-stu-id="5b285-225">Trapping all errors within an application and providing generic error messages, as well as enabling custom errors within IIS will help prevent information disclosure.</span></span> <span data-ttu-id="5b285-226">SQL Server-database en .NET-uitzonderingen afhandelt, onder andere foutafhandeling architecturen, zijn vooral uitgebreide en zeer nuttige tooa kwaadwillende gebruiker profileren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="5b285-226">SQL Server database and .NET Exception handling, among other error handling architectures, are especially verbose and extremely useful tooa malicious user profiling your application.</span></span> <span data-ttu-id="5b285-227">Voer niet direct weergegeven Hallo inhoud van een klasse is afgeleid van Hallo .NET uitzonderingsklasse en zorg ervoor dat de juiste uitzonderingsverwerking hebben zodat een onverwachte uitzondering per ongeluk wordt niet gegenereerd rechtstreeks toohello gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5b285-227">Do not directly display hello contents of a class derived from hello .NET Exception class, and ensure that you have proper exception handling so that an unexpected exception isn't inadvertently raised directly toohello user.</span></span></p><ul><li><span data-ttu-id="5b285-228">Geef algemene foutberichten rechtstreeks toohello-gebruiker die abstracte opslag specifieke gegevens rechtstreeks in het Hallo-bericht van uitzondering/fout</span><span class="sxs-lookup"><span data-stu-id="5b285-228">Provide generic error messages directly toohello user that abstract away specific details found directly in hello exception/error message</span></span></li><li><span data-ttu-id="5b285-229">Geen weergave Hallo inhoud van een .NET-uitzondering klasse rechtstreeks toohello gebruiker</span><span class="sxs-lookup"><span data-stu-id="5b285-229">Do not display hello contents of a .NET exception class directly toohello user</span></span></li><li><span data-ttu-id="5b285-230">Alle foutberichten afvangen en indien van toepassing hello gebruiker via een algemene fout bericht verzonden toohello toepassingsclient informeren</span><span class="sxs-lookup"><span data-stu-id="5b285-230">Trap all error messages and if appropriate inform hello user via a generic error message sent toohello application client</span></span></li><li><span data-ttu-id="5b285-231">Hallo-inhoud van hello uitzonderingsklasse niet blootstellen direct toohello gebruiker, met name Hallo retourwaarde van `.ToString()`, of Hallo-waarden van Hallo-bericht of StackTrace eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="5b285-231">Do not expose hello contents of hello Exception class directly toohello user, especially hello return value from `.ToString()`, or hello values of hello Message or StackTrace properties.</span></span> <span data-ttu-id="5b285-232">Veilig Meld deze informatie en een meer onschuldig bericht toohello gebruiker weergeven</span><span class="sxs-lookup"><span data-stu-id="5b285-232">Securely log this information and display a more innocuous message toohello user</span></span></li></ul>|

## <span data-ttu-id="5b285-233"><a id="default"></a>Standaard-fout tijdens het verwerken van pagina implementeren</span><span class="sxs-lookup"><span data-stu-id="5b285-233"><a id="default"></a>Implement Default error handling page</span></span>

| <span data-ttu-id="5b285-234">Titel</span><span class="sxs-lookup"><span data-stu-id="5b285-234">Title</span></span>                   | <span data-ttu-id="5b285-235">Details</span><span class="sxs-lookup"><span data-stu-id="5b285-235">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b285-236">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="5b285-236">**Component**</span></span>               | <span data-ttu-id="5b285-237">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="5b285-237">Web Application</span></span> | 
| <span data-ttu-id="5b285-238">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="5b285-238">**SDL Phase**</span></span>               | <span data-ttu-id="5b285-239">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="5b285-239">Build</span></span> |  
| <span data-ttu-id="5b285-240">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="5b285-240">**Applicable Technologies**</span></span> | <span data-ttu-id="5b285-241">Algemene</span><span class="sxs-lookup"><span data-stu-id="5b285-241">Generic</span></span> |
| <span data-ttu-id="5b285-242">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="5b285-242">**Attributes**</span></span>              | <span data-ttu-id="5b285-243">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="5b285-243">N/A</span></span>  |
| <span data-ttu-id="5b285-244">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="5b285-244">**References**</span></span>              | <span data-ttu-id="5b285-245">[Dialoogvenster voor instellingen van ASP.NET-foutpagina's bewerken](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span><span class="sxs-lookup"><span data-stu-id="5b285-245">[Edit ASP.NET Error Pages Settings Dialog Box](https://technet.microsoft.com/library/dd569096(WS.10).aspx)</span></span> |
| <span data-ttu-id="5b285-246">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="5b285-246">**Steps**</span></span> | <p><span data-ttu-id="5b285-247">Wanneer een ASP.NET-toepassing mislukt en zorgt ervoor dat een HTTP/1.x 500 Interne serverfout opgetreden of de configuratie van een onderdeel (zoals Aanvraagfiltering) voorkomt dat een pagina worden weergegeven, kunt u een foutbericht wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="5b285-247">When an ASP.NET application fails and causes an HTTP/1.x 500 Internal Server Error, or a feature configuration (such as Request Filtering) prevents a page from being displayed, an error message will be generated.</span></span> <span data-ttu-id="5b285-248">Beheerders kunnen kiezen of Hallo toepassing een bericht toohello client, gedetailleerde fout bericht toohello client of gedetailleerde fout bericht toolocalhost alleen moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5b285-248">Administrators can choose whether or not hello application should display a friendly message toohello client, detailed error message toohello client, or detailed error message toolocalhost only.</span></span> <span data-ttu-id="5b285-249">Hallo <customErrors> -label in het bestand web.config Hallo heeft drie beschikbare modi:</span><span class="sxs-lookup"><span data-stu-id="5b285-249">hello <customErrors> tag in hello web.config has three modes:</span></span></p><ul><li><span data-ttu-id="5b285-250">**Op:** geeft aan dat de aangepaste fouten zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5b285-250">**On:** Specifies that custom errors are enabled.</span></span> <span data-ttu-id="5b285-251">Als geen kenmerk defaultRedirect is opgegeven, zien gebruikers een algemene fout.</span><span class="sxs-lookup"><span data-stu-id="5b285-251">If no defaultRedirect attribute is specified, users see a generic error.</span></span> <span data-ttu-id="5b285-252">Hallo aangepaste fouten worden weergegeven toohello externe clients en de lokale host toohello</span><span class="sxs-lookup"><span data-stu-id="5b285-252">hello custom errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="5b285-253">**Uit:** geeft aan dat de aangepaste fouten zijn uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5b285-253">**Off:** Specifies that custom errors are disabled.</span></span> <span data-ttu-id="5b285-254">Hallo worden gedetailleerde ASP.NET-fouten weergegeven toohello externe clients en de lokale host toohello</span><span class="sxs-lookup"><span data-stu-id="5b285-254">hello detailed ASP.NET errors are shown toohello remote clients and toohello local host</span></span></li><li><span data-ttu-id="5b285-255">**RemoteOnly:** geeft aan dat aangepaste fouten alleen toohello externe clients worden weergegeven, en dat fouten in ASP.NET toohello lokale host worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5b285-255">**RemoteOnly:** Specifies that custom errors are shown only toohello remote clients, and that ASP.NET errors are shown toohello local host.</span></span> <span data-ttu-id="5b285-256">Dit is de standaardwaarde Hallo</span><span class="sxs-lookup"><span data-stu-id="5b285-256">This is hello default value</span></span></li></ul><p><span data-ttu-id="5b285-257">Open Hallo `web.config` voor toepassing hello/site en zorg ervoor dat Hallo-label een heeft `<customErrors mode="RemoteOnly" />` of `<customErrors mode="On" />` gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="5b285-257">Open hello `web.config` file for hello application/site and ensure that hello tag has either `<customErrors mode="RemoteOnly" />` or `<customErrors mode="On" />` defined.</span></span></p>|

## <span data-ttu-id="5b285-258"><a id="deployment"></a>Implementatiemethode tooRetail instellen in IIS</span><span class="sxs-lookup"><span data-stu-id="5b285-258"><a id="deployment"></a>Set Deployment Method tooRetail in IIS</span></span>

| <span data-ttu-id="5b285-259">Titel</span><span class="sxs-lookup"><span data-stu-id="5b285-259">Title</span></span>                   | <span data-ttu-id="5b285-260">Details</span><span class="sxs-lookup"><span data-stu-id="5b285-260">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b285-261">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="5b285-261">**Component**</span></span>               | <span data-ttu-id="5b285-262">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="5b285-262">Web Application</span></span> | 
| <span data-ttu-id="5b285-263">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="5b285-263">**SDL Phase**</span></span>               | <span data-ttu-id="5b285-264">Implementatie</span><span class="sxs-lookup"><span data-stu-id="5b285-264">Deployment</span></span> |  
| <span data-ttu-id="5b285-265">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="5b285-265">**Applicable Technologies**</span></span> | <span data-ttu-id="5b285-266">Algemene</span><span class="sxs-lookup"><span data-stu-id="5b285-266">Generic</span></span> |
| <span data-ttu-id="5b285-267">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="5b285-267">**Attributes**</span></span>              | <span data-ttu-id="5b285-268">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="5b285-268">N/A</span></span>  |
| <span data-ttu-id="5b285-269">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="5b285-269">**References**</span></span>              | <span data-ttu-id="5b285-270">[implementatie-Element (ASP.NET-instellingenschema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span><span class="sxs-lookup"><span data-stu-id="5b285-270">[deployment Element (ASP.NET Settings Schema)](https://msdn.microsoft.com/library/ms228298(VS.80).aspx)</span></span> |
| <span data-ttu-id="5b285-271">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="5b285-271">**Steps**</span></span> | <p><span data-ttu-id="5b285-272">Hallo `<deployment retail>` switch is bedoeld voor gebruik door IIS productieservers.</span><span class="sxs-lookup"><span data-stu-id="5b285-272">hello `<deployment retail>` switch is intended for use by production IIS servers.</span></span> <span data-ttu-id="5b285-273">Dit is de schakeloptie gebruikte toohelp toepassingen worden uitgevoerd met de best mogelijke prestaties Hallo en zo weinig mogelijk beveiligingsgegevens lekken door het uitschakelen van de toepassing mogelijkheid toogenerate traceringsuitvoer op een pagina uitschakelen Hallo mogelijkheid toodisplay Hallo gedetailleerde fout fouten opsporen switch berichten tooend gebruikers en Hallo uit te schakelen.</span><span class="sxs-lookup"><span data-stu-id="5b285-273">This switch is used toohelp applications run with hello best possible performance and least possible security information leakages by disabling hello application's ability toogenerate trace output on a page, disabling hello ability toodisplay detailed error messages tooend users, and disabling hello debug switch.</span></span></p><p><span data-ttu-id="5b285-274">Opties die ontwikkelaars zijn gericht, zijn zoals is mislukt, switches en vaak aanvragen tracering en foutopsporing zijn ingeschakeld tijdens het ontwikkelen van active.</span><span class="sxs-lookup"><span data-stu-id="5b285-274">Often times, switches and options that are developer-focused, such as failed request tracing and debugging, are enabled during active development.</span></span> <span data-ttu-id="5b285-275">Het verdient aanbeveling dat Hallo implementatiemethode op een productieserver tooretail wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5b285-275">It is recommended that hello deployment method on any production server be set tooretail.</span></span> <span data-ttu-id="5b285-276">Hallo machine.config-bestand te openen en zorg ervoor dat `<deployment retail="true" />` ingesteld tootrue blijft.</span><span class="sxs-lookup"><span data-stu-id="5b285-276">open hello machine.config file and ensure that `<deployment retail="true" />` remains set tootrue.</span></span></p>|

## <span data-ttu-id="5b285-277"><a id="fail"></a>Uitzonderingen zou moeten veilig mislukken</span><span class="sxs-lookup"><span data-stu-id="5b285-277"><a id="fail"></a>Exceptions should fail safely</span></span>

| <span data-ttu-id="5b285-278">Titel</span><span class="sxs-lookup"><span data-stu-id="5b285-278">Title</span></span>                   | <span data-ttu-id="5b285-279">Details</span><span class="sxs-lookup"><span data-stu-id="5b285-279">Details</span></span>      |
| ----------------------- | ------------ |
| <span data-ttu-id="5b285-280">**Onderdeel**</span><span class="sxs-lookup"><span data-stu-id="5b285-280">**Component**</span></span>               | <span data-ttu-id="5b285-281">Webtoepassing</span><span class="sxs-lookup"><span data-stu-id="5b285-281">Web Application</span></span> | 
| <span data-ttu-id="5b285-282">**SDL-fase**</span><span class="sxs-lookup"><span data-stu-id="5b285-282">**SDL Phase**</span></span>               | <span data-ttu-id="5b285-283">Ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="5b285-283">Build</span></span> |  
| <span data-ttu-id="5b285-284">**Van toepassing technologieën**</span><span class="sxs-lookup"><span data-stu-id="5b285-284">**Applicable Technologies**</span></span> | <span data-ttu-id="5b285-285">Algemene</span><span class="sxs-lookup"><span data-stu-id="5b285-285">Generic</span></span> |
| <span data-ttu-id="5b285-286">**Kenmerken**</span><span class="sxs-lookup"><span data-stu-id="5b285-286">**Attributes**</span></span>              | <span data-ttu-id="5b285-287">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="5b285-287">N/A</span></span>  |
| <span data-ttu-id="5b285-288">**Verwijzingen**</span><span class="sxs-lookup"><span data-stu-id="5b285-288">**References**</span></span>              | [<span data-ttu-id="5b285-289">Veilig mislukt</span><span class="sxs-lookup"><span data-stu-id="5b285-289">Fail securely</span></span>](https://www.owasp.org/index.php/Fail_securely) |
| <span data-ttu-id="5b285-290">**Stappen**</span><span class="sxs-lookup"><span data-stu-id="5b285-290">**Steps**</span></span> | <span data-ttu-id="5b285-291">Toepassing zou moeten veilig mislukken.</span><span class="sxs-lookup"><span data-stu-id="5b285-291">Application should fail safely.</span></span> <span data-ttu-id="5b285-292">Elke methode waarbij een Booleaanse waarde retourneert, op basis van welke bepaalde besluit wordt gemaakt, hebt uitzonderingsblok zorgvuldig gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5b285-292">Any method that returns a Boolean value, based on which certain decision is made, should have exception block carefully created.</span></span> <span data-ttu-id="5b285-293">Er zijn veel logische fouten vanwege toowhich beveiliging problemen kneep in wanneer Hallo uitzonderingsblok ondoordacht is geschreven.</span><span class="sxs-lookup"><span data-stu-id="5b285-293">There are lot of logical errors due toowhich security issues creep in, when hello exception block is written carelessly.</span></span>|

### <a name="example"></a><span data-ttu-id="5b285-294">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5b285-294">Example</span></span>
```C#
        public static bool ValidateDomain(string pathToValidate, Uri currentUrl)
        {
            try
            {
                if (!string.IsNullOrWhiteSpace(pathToValidate))
                {
                    var domain = RetrieveDomain(currentUrl);
                    var replyPath = new Uri(pathToValidate);
                    var replyDomain = RetrieveDomain(replyPath);

                    if (string.Compare(domain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                    {
                        //// Adding additional check tooenable CMS urls if they are not hosted on same domain.
                        if (!string.IsNullOrWhiteSpace(Utilities.CmsBase))
                        {
                            var cmsDomain = RetrieveDomain(new Uri(Utilities.Base.Trim()));
                            if (string.Compare(cmDomain, replyDomain, StringComparison.OrdinalIgnoreCase) != 0)
                            {
                                return false;
                            }
                            else
                            {
                                return true;
                            }
                        }

                        return false;
                    }
                }

                return true;
            }
            catch (UriFormatException ex)
            {
                LogHelper.LogException("Utilities:ValidateDomain", ex);
                return true;
            }
        }
```
<span data-ttu-id="5b285-295">Hallo hierboven methode retourneert True, wordt altijd als een uitzondering gebeurt.</span><span class="sxs-lookup"><span data-stu-id="5b285-295">hello above method will always return True, if some exception happens.</span></span> <span data-ttu-id="5b285-296">Als de eindgebruiker Hallo een verkeerd ingedeelde URL biedt, die browser respecteert Hallo, maar Hallo `Uri()` constructor niet, dit wordt Veroorzaak een exception en Hallo slachtoffer toohello geldig, maar een verkeerd ingedeelde URL worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5b285-296">If hello end user provides a malformed URL, that hello browser respects, but hello `Uri()` constructor doesn't, this will throw an exception, and hello victim will be taken toohello valid but malformed URL.</span></span> 

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
# <a name="customize-swashbuckle-generated-api-definitions"></a>Door Swashbuckle gegenereerde API-definities aanpassen
## <a name="overview"></a>Overzicht
Dit artikel wordt uitgelegd hoe toocustomize Swashbuckle toohandle algemene scenario's waarin u tooalter kunt standaardgedrag Hallo:

* Swashbuckle dubbele bewerkings-id's voor overloads van methoden van de domeincontroller genereert
* Swashbuckle wordt ervan uitgegaan dat Hallo alleen geldig antwoord van een methode HTTP 200 (OK is) 

## <a name="customize-operation-identifier-generation"></a>Bewerking-ID generatie aanpassen
Swashbuckle genereert Swagger bewerking-id's door de naam van de domeincontroller en de methodenaam van de cookievalidatie. Dit patroon maakt een probleem wanneer u meerdere overloads van een methode hebt: Swashbuckle dubbele bewerkings-id's, genereert, dit ongeldig Swagger JSON is.

Bijvoorbeeld, Hallo na controllercode zorgt ervoor dat Swashbuckle toogenerate drie Contact_Get bewerking-id's.

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

U kunt handmatig Hallo probleem oplossen door middel van een unieke namen, zoals de volgende Hallo voor dit voorbeeld Hallo methoden:

* Ophalen
* GetById
* GetPage

Hallo alternatief is tooextend Swashbuckle toomake deze unieke bewerkings-id's voor het automatisch genereren.

Hallo volgende stappen laten zien hoe toocustomize Swashbuckle met behulp van Hallo *SwaggerConfig.cs* -bestand dat is opgenomen in Hallo project door de projectsjabloon Hallo-Preview voor Visual Studio-API-Apps.  U kunt ook Swashbuckle in een Web-API-project dat u voor implementatie als een API-app configureert aanpassen.

1. Maak een aangepast `IOperationFilter` implementatie 
   
    Hallo `IOperationFilter` interface biedt een uitbreidbaar punt voor Swashbuckle-gebruikers die toocustomize verschillende aspecten van Hallo Swagger-metagegevens proces. Hallo toont volgende code een methode van het gedrag van de generatie-id-bewerking Hallo wijzigen. Hallo-code worden namen toohello bewerking-id parameternaam toegevoegd.  
   
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
2. In *App_Start\SwaggerConfig.cs* bestand, aanroep Hallo `OperationFilter` methode toocause Swashbuckle toouse Hallo nieuwe `IOperationFilter` implementatie.
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    Hallo *SwaggerConfig.cs* -bestand dat is verwijderd door Hallo Swashbuckle NuGet-pakket bevat veel opmerkingen out voorbeelden van uitbreidbaarheidspunten. Hallo aanvullende opmerkingen worden hier niet weergegeven. 
   
    Nadat u deze wijziging aanbrengt uw `IOperationFilter` implementatie wordt gebruikt en zorgt ervoor dat unieke bewerkings-id's toobe gegenereerd.
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>Reactiecodes dan 200 toestaan
Standaard Swashbuckle wordt ervan uitgegaan dat een HTTP 200 (OK) antwoord Hallo *alleen* rechtmatige reactie van een Web-API-methode. In sommige gevallen kunt u tooreturn overige reactiecodes zonder Hallo client tooraise een uitzondering veroorzaakt.  Bijvoorbeeld, hello volgende Web-API code toont een scenario waarin u Hallo client tooaccept zou willen een 200 of een 404 als geldige antwoorden.

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

In dit scenario bevat Hallo Swagger die Swashbuckle standaard genereert slechts één legitieme HTTP-statuscode HTTP 200.

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

Omdat Hallo Swagger API-definitie toogenerate code Visual Studio voor de client hello gebruikt, maakt het clientcode die een uitzondering voor een antwoord dan een HTTP 200 genereert. Hallo-code hieronder is van een C#-client gegenereerd voor deze voorbeeld-Web-API-methode.

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

Swashbuckle biedt twee manieren aan te passen Hallo-lijst van verwachte HTTP-antwoordcodes die wordt gegenereerd met XML-commentaar of Hallo `SwaggerResponse` kenmerk. Hallo-kenmerk is gemakkelijker, maar is alleen beschikbaar in Swashbuckle 5.1.5 of hoger. Hallo API Apps preview nieuw project in Visual Studio 2013 bevat Swashbuckle versie 5.0.0, dus als u Hallo-sjabloon gebruikt en niet dat tooupdate Swashbuckle wilt, de enige optie toouse XML-commentaar. 

### <a name="customize-expected-response-codes-using-xml-comments"></a>Verwachte reactiecodes met XML-commentaar aanpassen
Gebruik deze methode toospecify antwoordcodes als uw Swashbuckle-versie ouder dan 5.1.5 is.

1. Voeg eerst de XML-documentopmerkingen via Hallo-methoden die u wenst toospecify HTTP-antwoordcodes voor. Verholpen Hallo voorbeeld-Web-API hierboven weergegeven en die van toepassing hello XML-documentatie tooit zou leiden tot code zoals Hallo voorbeeld te volgen. 
   
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
2. Toevoegen van de instructies in Hallo *SwaggerConfig.cs* toodirect Swashbuckle toomake gebruik van de XML-documentatiebestand Hallo-bestand.
   
   * Open *SwaggerConfig.cs* en maakt u een methode op Hallo *SwaggerConfig* klasse toospecify Hallo pad toohello XML-documentatiebestand. 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Schuif omlaag in Hallo *SwaggerConfig.cs* totdat er Hallo opmerkingen out coderegel die lijkt op de onderstaande schermafdruk Hallo-bestand. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * Verwijder de opmerkingen in Hallo regel tooenable Hallo XML-commentaar verwerking tijdens het genereren van Swagger. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. Ga naar eigenschappen van het project Hallo in volgorde toogenerate Hallo XML-documentatiebestand, en Hallo XML-documentatiebestand zoals weergegeven in onderstaande schermafbeelding voor Hallo inschakelen. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

Nadat u deze stappen hebt uitgevoerd, bevatten Hallo Swagger JSON die worden gegenereerd door Swashbuckle Hallo HTTP-antwoordcodes die u hebt opgegeven in Hallo XML-opmerkingen. Hallo onderstaande schermafbeelding ziet u deze nieuwe JSON-nettolading. 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

Wanneer u Visual Studio tooregenerate Hallo clientcode voor uw REST API, accepteert Hallo C#-code beide statuscodes Hallo HTTP OK en niet gevonden zonder een uitzondering, zodat uw consumerende code toomake beslissingen op hoe toohandle Hallo retourneren van een null-waarde Neem contact op met een record. 

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

Hallo-code voor deze demonstratie kunt u vinden in [deze GitHub-opslagplaats](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse). Samen met de Hallo Web-API is gemarkeerd met XML-documentopmerkingen project een consoletoepassingsproject die een gegenereerde client voor deze API bevat. 

### <a name="customize-expected-response-codes-using-hello-swaggerresponse-attribute"></a>Verwachte reactiecodes met Hallo SwaggerResponse kenmerk aanpassen
Hallo [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) kenmerk is beschikbaar in Swashbuckle 5.1.5 en hoger. Als u een eerdere versie in uw project hebt, wordt in deze sectie begint met het waarin wordt uitgelegd hoe tooupdate hello Swashbuckle NuGet-pakket zodat u kunt dit kenmerk.

1. In **Solution Explorer**, met de rechtermuisknop op uw Web API-project en klik op **NuGet-pakketten beheren**. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. Klik op Hallo *Update* knop volgende toohello *Swashbuckle* NuGet-pakket. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. Hallo toevoegen *SwaggerResponse* toohello Web API-actiemethoden waarvoor u toospecify geldig HTTP-antwoordcodes wilt kenmerken. 
   
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
4. Voeg een `using` -instructie voor het Hallo-kenmerk namespace:
   
        using Swashbuckle.Swagger.Annotations;
5. Blader toohello */swagger/docs/v1* URL van uw project en verschillende HTTP-antwoordcodes zijn zichtbaar in Hallo Hallo Swagger JSON. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

Hallo-code voor deze demonstratie kunt u vinden in [deze GitHub-opslagplaats](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes). Samen met de Hallo Web API-project gedecoreerd worden met Hallo *SwaggerResponse* kenmerk is een consoletoepassingsproject die een gegenereerde client voor deze API bevat. 

## <a name="next-steps"></a>Volgende stappen
In dit artikel heeft geleerd hoe toocustomize Hallo manier Swashbuckle bewerking-id's en geldig reactiecodes genereert. Zie voor meer informatie [Swashbuckle op GitHub](https://github.com/domaindrivendev/Swashbuckle).


---
title: Door Swashbuckle gegenereerde API-definities aanpassen
description: Informatie over het aanpassen van Swagger API-definities die worden gegenereerd door Swashbuckle voor een API-app in Azure App Service.
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
ms.openlocfilehash: c83905a97fb2ee988fe06fc1f9a7379c1741fd02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="customize-swashbuckle-generated-api-definitions"></a>Door Swashbuckle gegenereerde API-definities aanpassen
## <a name="overview"></a>Overzicht
In dit artikel wordt uitgelegd hoe Swashbuckle voor het afhandelen van algemene scenario's mogelijk waar u het standaardgedrag alter aanpassen:

* Swashbuckle dubbele bewerkings-id's voor overloads van methoden van de domeincontroller genereert
* Swashbuckle wordt ervan uitgegaan dat de enige geldige reactie van een methode HTTP 200 (OK) 

## <a name="customize-operation-identifier-generation"></a>Bewerking-ID generatie aanpassen
Swashbuckle genereert Swagger bewerking-id's door de naam van de domeincontroller en de methodenaam van de cookievalidatie. Dit patroon maakt een probleem wanneer u meerdere overloads van een methode hebt: Swashbuckle dubbele bewerkings-id's, genereert, dit ongeldig Swagger JSON is.

De volgende code van de domeincontroller wordt bijvoorbeeld Swashbuckle drie Contact_Get bewerking-id's genereren.

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsincode.png)

![](./media/app-service-api-dotnet-swashbuckle-customize/multiplegetsinjson.png)

U kunt handmatig het probleem oplossen door middel van de methoden unieke namen, zoals de volgende onderwerpen voor dit voorbeeld:

* Ophalen
* GetById
* GetPage

Het alternatief is om uit te breiden Swashbuckle om deze unieke bewerkings-id's automatisch te genereren.

De volgende stappen laten zien hoe Swashbuckle aanpassen met behulp van de *SwaggerConfig.cs* -bestand dat is opgenomen in het project door de projectsjabloon Visual Studio API Apps-Preview.  U kunt ook Swashbuckle in een Web-API-project dat u voor implementatie als een API-app configureert aanpassen.

1. Maak een aangepast `IOperationFilter` implementatie 
   
    De `IOperationFilter` interface biedt een uitbreidbaar punt voor Swashbuckle-gebruikers die u wilt aanpassen van verschillende aspecten van het proces Swagger-metagegevens. De volgende code toont een methode van het wijzigen van het gedrag van de generatie-id-bewerking. De code voegt parameternamen met de naam van de bewerking-id.  
   
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
2. In *App_Start\SwaggerConfig.cs* bestand, Roep de `OperationFilter` Swashbuckle voor het gebruik van de nieuwe hierbij `IOperationFilter` implementatie.
   
        c.OperationFilter<MultipleOperationsWithSameVerbFilter>();
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/usefilter.png)
   
    De *SwaggerConfig.cs* -bestand dat door het Swashbuckle NuGet-pakket is verwijderd veel opmerkingen out voorbeelden van uitbreidbaarheidspunten bevat. Aanvullende opmerkingen worden hier niet weergegeven. 
   
    Nadat u deze wijziging aanbrengt uw `IOperationFilter` implementatie wordt gebruikt en zorgt ervoor dat unieke bewerkings-id's die worden gegenereerd.
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/uniqueids.png)

<a id="multiple-response-codes" name="multiple-response-codes"></a>

## <a name="allow-response-codes-other-than-200"></a>Reactiecodes dan 200 toestaan
Standaard Swashbuckle wordt ervan uitgegaan dat een HTTP 200 (OK) antwoord de *alleen* rechtmatige reactie van een Web-API-methode. In sommige gevallen wilt u mogelijk andere retourcodes antwoord zonder dat de client een uitzondering worden gegenereerd.  De volgende Web-API-code laat bijvoorbeeld een scenario waarin u de client een 200 of een 404 als geldige antwoorden te aanvaarden zou willen zien.

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

In dit scenario bevat de Swagger die Swashbuckle standaard genereert slechts één legitieme HTTP-statuscode HTTP 200.

![](./media/app-service-api-dotnet-swashbuckle-customize/http-200-output-only.png)

Omdat de Swagger API-definitie Visual Studio gebruikt voor het genereren van code voor de client, maakt het clientcode die een uitzondering voor een antwoord dan een HTTP 200 genereert. De volgende code is van een C#-client gegenereerd voor deze voorbeeld-Web-API-methode.

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

Swashbuckle biedt twee manieren voor het aanpassen van de lijst met verwachte HTTP-antwoordcodes die wordt gegenereerd met behulp van XML-commentaar of het `SwaggerResponse` kenmerk. Het kenmerk is gemakkelijker, maar is alleen beschikbaar in Swashbuckle 5.1.5 of hoger. De sjabloon API Apps preview nieuw project in Visual Studio 2013 omvat Swashbuckle versie 5.0.0, dus als u de sjabloon gebruikt en niet wilt bijwerken Swashbuckle, de enige optie is het gebruik van XML-commentaar. 

### <a name="customize-expected-response-codes-using-xml-comments"></a>Verwachte reactiecodes met XML-commentaar aanpassen
Gebruik deze methode reactiecodes opgeven als uw Swashbuckle-versie ouder dan 5.1.5 is.

1. Voeg eerst via de methoden die u wilt opgeven van HTTP-antwoordcodes voor XML-documentopmerkingen toe. De voorbeeld-Web-API nemen zou actie hierboven weergegeven en de XML-documentatie toe te passen leiden tot code op het volgende voorbeeld. 
   
        /// <summary>
        /// Returns the specified contact.
        /// </summary>
        /// <param name="id">The ID of the contact.</param>
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
2. Toevoegen van de instructies in de *SwaggerConfig.cs* te leiden Swashbuckle gebruik te maken van de XML documentatiebestand.
   
   * Open *SwaggerConfig.cs* en maakt u een methode in de *SwaggerConfig* -klasse moet het pad naar het XML-documentatiebestand opgeven. 
     
           private static string GetXmlCommentsPath()
           {
               return string.Format(@"{0}\XmlComments.xml", 
                   System.AppDomain.CurrentDomain.BaseDirectory);
           }
   * Schuif omlaag de *SwaggerConfig.cs* bestand totdat u de regel opmerkingen-out van code die lijkt op de onderstaande schermafbeelding ziet. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-commented-out.png)
   * Verwijder de opmerkingen in de regel voor het inschakelen van de XML-commentaar verwerking tijdens het genereren van Swagger. 
     
       ![](./media/app-service-api-dotnet-swashbuckle-customize/xml-comments-uncommented.png)
3. Om het XML-documentatiebestand genereren, Ga naar eigenschappen van het project en inschakelen van de XML-documentatiebestand zoals weergegeven in de onderstaande schermafbeelding. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/enable-xml-documentation-file.png) 

Nadat u deze stappen hebt uitgevoerd, wordt in de Swagger JSON die wordt gegenereerd door Swashbuckle de HTTP-antwoordcodes die u hebt opgegeven in de XML-commentaar weerspiegelen. De onderstaande schermafbeelding ziet u deze nieuwe JSON-nettolading. 

![](./media/app-service-api-dotnet-swashbuckle-customize/swagger-multiple-responses.png)

Wanneer u Visual Studio opnieuw de clientcode genereren voor de REST-API gebruikt, accepteert de C#-code de HTTP-OK en niet gevonden statuscodes zonder een uitzondering, zodat uw code in beslag nemen om beslissingen te nemen over het afhandelen van het retourneren van een record voor een null contactpersoon. 

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

De code voor deze demonstratie kunt u vinden in [deze GitHub-opslagplaats](https://github.com/Azure-Samples/app-service-api-dotnet-swashbuckle-swaggerresponse). Samen met de Web-API is gemarkeerd met XML-documentopmerkingen project een consoletoepassingsproject die een gegenereerde client voor deze API bevat. 

### <a name="customize-expected-response-codes-using-the-swaggerresponse-attribute"></a>Verwachte reactiecodes met het kenmerk SwaggerResponse aanpassen
De [SwaggerResponse](https://github.com/domaindrivendev/Swashbuckle/blob/master/Swashbuckle.Core/Swagger/Annotations/SwaggerResponseAttribute.cs) kenmerk is beschikbaar in Swashbuckle 5.1.5 en hoger. Als u een eerdere versie in uw project hebt, wordt in deze sectie begint met het waarin wordt uitgelegd hoe het Swashbuckle NuGet-pakket bijwerken zodat u dit kenmerk kunt.

1. In **Solution Explorer**, met de rechtermuisknop op uw Web API-project en klik op **NuGet-pakketten beheren**. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/manage-nuget-packages.png)
2. Klik op de *Update* naast de *Swashbuckle* NuGet-pakket. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/update-nuget-dialog.png)
3. Voeg de *SwaggerResponse* kenmerken aan de Web-API actiemethoden waarvoor u wilt geldig HTTP-antwoord-codes opgeven. 
   
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
4. Voeg een `using` -instructie voor het kenmerk namespace:
   
        using Swashbuckle.Swagger.Annotations;
5. Blader naar de */swagger/docs/v1* URL van uw project en de verschillende HTTP-antwoord-codes zijn zichtbaar in de Swagger JSON. 
   
    ![](./media/app-service-api-dotnet-swashbuckle-customize/multiple-responses-post-attributes.png)

De code voor deze demonstratie kunt u vinden in [deze GitHub-opslagplaats](https://github.com/Azure-Samples/API-Apps-DotNet-Swashbuckle-Customization-MultipleResponseCodes-With-Attributes). Samen met de Web API-project gedecoreerd worden met de *SwaggerResponse* kenmerk is een consoletoepassingsproject die een gegenereerde client voor deze API bevat. 

## <a name="next-steps"></a>Volgende stappen
In dit artikel is het aanpassen van de manier waarop die swashbuckle bewerking-id's en geldig antwoord-codes genereert weergegeven. Zie voor meer informatie [Swashbuckle op GitHub](https://github.com/domaindrivendev/Swashbuckle).


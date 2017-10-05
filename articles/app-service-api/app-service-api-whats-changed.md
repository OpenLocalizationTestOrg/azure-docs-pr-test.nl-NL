---
title: App Service API Apps - wat er gewijzigd | Microsoft Docs
description: Ontdek wat er nieuw voor API-Apps in Azure App Service.
services: app-service\api
documentationcenter: .net
author: mohitsriv
manager: erikre
editor: tdykstra
ms.assetid: a9b58066-e8fd-48b8-a651-4613b1736433
ms.service: app-service-api
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: rachelap
ms.openlocfilehash: e4e25f2cd1d39bb0113e3fe2bc37120f92227b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="app-service-api-apps---whats-changed"></a>App Service API Apps - wat er gewijzigd
Op de Connect ()-gebeurtenis in November 2015, een aantal verbeteringen in Azure App Service zijn [aangekondigd](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/). Deze verbeteringen bestaan onder andere onderliggende wijzigingen in API-Apps beter uitgelijnd met mobiele en Web-Apps, aantal concept beperken en de implementatie en runtime-prestaties verbeteren. Starten van de nieuwe API-apps 30 November 2015 u maakt met behulp van de Azure-beheerportal of de meest recente tooling worden deze wijzigingen worden doorgevoerd. Dit artikel worden deze wijzigingen, evenals hoe u bestaande apps om te profiteren van de mogelijkheden te implementeren.

## <a name="feature-changes"></a>Functionele wijzigingen
De belangrijkste functies van API Apps – verificatie, CORS en API-metagegevens – hebt verplaatst, rechtstreeks in App Service. Met deze wijziging, de functies zijn beschikbaar via het Web, mobiel en API-Apps. In feite alle drie delen dezelfde **Microsoft.Web/sites** brontype in Resource Manager. De API-Apps-gateway is niet langer nodig is of die worden aangeboden met API-Apps. Dit is het eenvoudiger Azure API Management gebruikt, omdat er alleen de één API Management-gateway worden.

![Overzicht van de API-Apps](./media/app-service-api-whats-changed/api-apps-overview.png)

Een belangrijke ontwerpprincipe met de API-Apps-update is zodat u laat uw API is in de taal van keuze kunt maken.  Als uw API wordt al geïmplementeerd als een Web-App of mobiele Apps, hoeft u niet opnieuw implementeren van uw app om te profiteren van de nieuwe functies. Als u momenteel preview-API-Apps, wordt migratie richtlijnen hieronder beschreven.

### <a name="authentication"></a>Authentication
De bestaande klare API-Apps, Mobile Services/Apps en Web-Apps verificatiefuncties hebben is unified en beschikbaar zijn in een enkel Azure App Service-verificatie-blade in de beheerportal. Zie voor een inleiding tot verificatieservices in App Service, [uitbreiden van App Service-verificatie / autorisatie](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

Er zijn een aantal relevante nieuwe mogelijkheden voor API-scenario's:

* **Ondersteuning voor het gebruik van Azure Active Directory rechtstreeks**, zonder clientcode hebben voor het uitwisselen van de AAD-token voor een sessietoken: de client kan alleen de AAD-tokens in de autorisatie-header bevatten volgens de specificatie van bearer-token. Dit betekent ook dat er is geen App Service-specifiek SDK aan de kant van de client of server is vereist. 
* **Service-naar-service of 'Interne' toegang**: als u een daemon-proces of enige andere client toegang tot API's zonder een interface nodig hebt, kunt u een token met een AAD-service-principal aanvragen en doorgeven aan de App Service voor verificatie met uw toepassing.
* **Autorisatie uitgesteld**: veel toepassingen hebben verschillende toegangsbeperkingen voor verschillende onderdelen van de toepassing. Misschien wilt u bepaalde API's zijn openbaar, terwijl andere aanmelden vereisen. De oorspronkelijke functie van verificatie/autorisatie is ofwel volledig, ofwel, met de gehele site aanmelding vereisen. Deze optie nog bestaat, maar u kunt ook toestaan dat de toepassingscode toegang beslissingen weergeven nadat de gebruiker heeft geverifieerd door App Service.

Zie voor meer informatie over de nieuwe verificatiefuncties [verificatie en autorisatie voor API-Apps in Azure App Service](app-service-api-authentication.md). Zie voor meer informatie over het migreren van bestaande API-apps uit het vorige model van de API-apps naar de nieuwe [migreren bestaande API apps](#migrating-existing-api-apps) verderop in dit artikel.

### <a name="cors"></a>CORS
In plaats van een door komma's gescheiden **MS_CrossDomainOrigins** app instelt, er is nu een blade in de Azure-beheerportal voor het configureren van CORS. U kunt ook kunnen worden geconfigureerd met Resource Manager tooling zoals Azure PowerShell, CLI of [Resource Explorer](https://resources.azure.com/). Stel de **cors** -eigenschap op de **Microsoft.Web/sites/config** resourcetype voor uw  **&lt;sitenaam&gt;/web-** resource. Bijvoorbeeld:

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>API-metagegevens
De blade API-definitie is nu beschikbaar via het Web, mobiel en API-Apps. In de beheerportal kunt u een relatieve url of een absolute url die verwijst naar een eindpunt dat hosts een Swagger 2.0-weergave van uw API. U kunt ook kunnen worden geconfigureerd met Resource Manager tooling. Stel de **apiDefinition** -eigenschap op de **Microsoft.Web/sites/config** resourcetype voor uw  **&lt;sitenaam&gt;/web-** resource. Bijvoorbeeld:

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

Op dit moment moet het metagegevenseindpunt openbaar toegankelijk zijn zonder verificatie voor veel downstream-clients (bijvoorbeeld Visual Studio REST API client genereren en PowerApps 'API toevoegen' stroom) deze wordt gebruikt. Dit betekent dat als u App Service-verificatie gebruikt en beschikbaar wilt maken van de API-definitie van uw app zelf, moet u de eerder beschreven, zodat de route naar uw Swagger-metagegevens openbaar is uitgesteld verificatie-optie te gebruiken.

## <a name="management-portal"></a>Management Portal
Selecteren **Nieuw > Web + mobiel > API-App** maken in de portal voor API-apps die overeenkomen met de nieuwe mogelijkheden die zijn beschreven in het artikel. **Bladeren > API-Apps** wordt alleen deze nieuwe API-apps. Als u naar een API-app bladeren, wordt de blade deelt dezelfde indeling en mogelijkheden als die van de Web- en mobiele Apps. De enige verschillen zijn Quick Start-inhoud en ordening van instellingen.

Bestaande API-apps (of Marketplace-API-apps die zijn gemaakt op basis van Logic Apps) met het vorige voorbeeld mogelijkheden nog steeds zichtbaar in de ontwerpfunctie voor Logic Apps en bij het bladeren door alle resources in een resourcegroep.

## <a name="visual-studio"></a>Visual Studio
De meeste Web-Apps tooling geschikt is voor de nieuwe API-apps omdat ze de dezelfde onderliggende delen **Microsoft.Web/sites** brontype. De Azure Visual Studio tooling, echter moet worden bijgewerkt naar versie 2.8.1 of later omdat een aantal mogelijkheden die specifiek zijn voor de API's worden getoond. Download de SDK van de [pagina Azure downloads](https://azure.microsoft.com/downloads/).

Publiceren met de optimalisatie van de App Service-typen is ook unified onder **publiceren > Microsoft Azure App Service**:

![API-Apps publiceren](./media/app-service-api-whats-changed/api-apps-publish.png)

Lees de aankondiging voor meer informatie over SDK 2.8.1 [blogbericht](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).

U kunt het publicatieprofiel dat u kunt ook handmatig importeren vanuit de beheerportal publiceren inschakelen. Echter Cloud Explorer, genereren van code en API Apps selectie/maken SDK 2.8.1 vereist of hoger.

## <a name="migrating-existing-api-apps"></a>Migreren van bestaande API-apps
Als uw aangepaste API wordt geïmplementeerd naar de vorige Preview-versie van API Apps, vragen wij dat u naar het nieuwe model voor API-Apps met 31 December 2015 migreert. Omdat zowel het oude en nieuwe model zijn gebaseerd op Web-API's die worden gehost in App Service, het merendeel van de bestaande code opnieuw kan worden gebruikt.

### <a name="hosting-and-redeployment"></a>Host en opnieuw implementeren
De stappen voor het distribueren van zijn hetzelfde als het implementeren van een bestaande Web-API in App Service. stappen:

1. Maak een lege API-app. Dit is mogelijk in de portal met New > API-App in Visual Studio van publiceren, of van Resource Manager tooling. Als Resource Manager tooling of sjablonen, stelt u de **soort** van waarde naar **api** op de **Microsoft.Web/sites** brontype naar snelstartgidsen en instellingen in de beheerportal gericht op API-scenario's hebben.
2. Verbinding maken en implementeren van uw project in de lege API-app met behulp van een van de implementatie-mechanismen ondersteund door App Service. Lees [documentatie van Azure App Service-implementatie](../app-service-web/web-sites-deploy.md) voor meer informatie. 

### <a name="authentication"></a>Authentication
De App Service-verificatieservices ondersteuning voor dezelfde mogelijkheden die beschikbaar zijn met het vorige model van de API-Apps die waren. Als u sessie tokens en behoefte hebt aan SDK's, gebruikt u de volgende client- en SDK's:

* Client: [Azure mobiele Client SDK](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* Server: [Microsoft Azure mobiele App .NET-authenticatie-extensie](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

Als u in plaats daarvan de alfa-App Service SDK's zijn gebruikt, worden deze nu afgeschafte:

* Client: [AppService-SDK van Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* Server: [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

In het bijzonder met Azure Active Directory is geen App Service-specifieke echter vereist als u de AAD-token rechtstreeks.

### <a name="internal-access"></a>Interne toegang
Het vorige model van de API-Apps een ingebouwde interne toegangsniveau opgenomen. Dit gebruik van de SDK vereist voor het ondertekenen van aanvragen. Zoals eerder beschreven, met het nieuwe model van de API-Apps kunnen AAD-service-principals worden gebruikt als alternatief voor verificatie van de service to service zonder dat een App Service-specifiek SDK. Meer informatie [principal verificatie van de Service voor API Apps in Azure App Service](app-service-api-dotnet-service-principal-auth.md).

### <a name="discovery"></a>Detectie
Het vorige model van de API-Apps had API's voor het detecteren van andere API-apps tijdens runtime in dezelfde resourcegroep achter dezelfde gateway. Dit is vooral nuttig in architecturen die microservice patronen te implementeren. Hoewel dit niet rechtstreeks wordt ondersteund, zijn een aantal opties zijn beschikbaar:

1. Gebruik de Azure Resource Manager-API voor detectie.
2. Azure API Management voor uw API-App Service gehost's geplaatst. Azure API Management fungeert als een façade en een stabiele externe gerichte url kunt opgeven, zelfs als u interne topologie verandert.
3. Uw eigen detectie API-app bouwen en andere registreren bij de detectie-app op het starten van de API-apps hebben.
4. Vul de eindpunten van de API-apps de instellingen van de app van alle API-apps (en clients) tijdens de implementatie. Dit is beschikbaar in de sjabloon implementaties en de API-Apps kunt u nu besturingselement van de url.

## <a name="using-api-apps-with-logic-apps"></a>Met behulp van API-Apps met Logic Apps
Het nieuwe model van de API-apps werkt goed samen met [schemaversie 2015-08-01 van Logic Apps](../logic-apps/logic-apps-schema-2015-08-01.md).

## <a name="next-steps"></a>Volgende stappen
Lees voor meer informatie de artikelen in de [API Apps-documentatierubriek](https://azure.microsoft.com/documentation/services/app-service/api/). Ze zijn bijgewerkt naar aanleiding van het nieuwe model voor API-Apps. Bovendien bereiken in de forums voor meer informatie of instructies voor migratie:

* [MSDN-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-api-apps)


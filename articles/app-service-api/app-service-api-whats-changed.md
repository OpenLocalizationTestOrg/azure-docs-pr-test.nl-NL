---
title: aaaApp Service API Apps - wat er gewijzigd | Microsoft Docs
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
ms.openlocfilehash: 79df54f1dae91d7c5d3b66d208d0d1c1d7d55ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-api-apps---whats-changed"></a>App Service API Apps - wat er gewijzigd
Hallo Connect ()-gebeurtenis in November 2015, een aantal verbeteringen tooAzure App Service zijn [aangekondigd](https://azure.microsoft.com/blog/azure-app-service-updates-november-2015/). Deze verbeteringen bestaan onder andere onderliggende wijzigingen tooAPI Apps toobetter uitgelijnd met mobiele en Web-Apps, concept aantal en de implementatie en runtime worden verbeterd. 30 November 2015, nieuwe API-apps starten u maakt met behulp van hello Azure-beheerportal of de meest recente tooling Hallo worden deze wijzigingen worden doorgevoerd. In dit artikel deze wijzigingen worden beschreven, evenals hoe tooredeploy bestaande apps tootake gebruik van Hallo-mogelijkheden.

## <a name="feature-changes"></a>Functionele wijzigingen
Hallo belangrijke functies van API Apps – verificatie, CORS en API-metagegevens – hebt verplaatst, rechtstreeks in App Service. Met deze wijziging Hallo functies zijn beschikbaar via het Web, mobiel en API-Apps. In feite alle drie delen dezelfde Hallo **Microsoft.Web/sites** brontype in Resource Manager. Hallo API Apps gateway is niet langer nodig is of die worden aangeboden met API-Apps. Dit maakt het ook eenvoudiger toouse Azure API Management aangezien er net Hallo enkele API Management-gateway.

![Overzicht van de API-Apps](./media/app-service-api-whats-changed/api-apps-overview.png)

Een belangrijke ontwerpprincipe Hello API Apps bijwerken is tooenable toobring u uw API ongewijzigd in de taal van keuze is.  Als uw API wordt al geïmplementeerd als een Web-App of mobiele Apps, hoeft u geen tooredeploy uw app tootake profiteren van nieuwe functies Hallo. Als u momenteel preview-API-Apps, wordt migratie richtlijnen hieronder beschreven.

### <a name="authentication"></a>Authentication
Hallo bestaande klare API-Apps, Mobile Services/Apps en Web-Apps verificatiefuncties hebben is unified en zijn beschikbaar in een enkel Azure App Service-verificatie-blade in de beheerportal Hallo. Zie voor een inleiding tooauthentication services in App Service, [uitbreiden van App Service-verificatie / autorisatie](https://azure.microsoft.com/blog/announcing-app-service-authentication-authorization/).

Er zijn een aantal relevante nieuwe mogelijkheden voor API-scenario's:

* **Ondersteuning voor het gebruik van Azure Active Directory rechtstreeks**, zonder clientcode tooexchange Hallo AAD-token voor een sessietoken hebben: de client alleen in kunt opnemen Hallo AAD tokens Hallo-autorisatie-header volgens toohello bearer-token specificatie. Dit betekent ook dat er geen SDK -App Service-specifieke is vereist op Hallo client of server side. 
* **Service-naar-service of 'Interne' toegang**: als u een daemon-proces of sommige andere client die toegang tooAPIs zonder een interface hebt, kunt u een token met een AAD-service-principal aanvragen en geef dit tooApp Service voor verificatie met uw de toepassing.
* **Autorisatie uitgesteld**: veel toepassingen hebben verschillende toegangsbeperkingen voor verschillende onderdelen van de toepassing hello. Misschien wilt u bepaalde API's toobe openbaar, terwijl andere aanmelden vereisen. Hallo oorspronkelijke verificatie/autorisatie-functie is ofwel volledig, ofwel, met de gehele site Hallo aanmelding vereisen. Deze optie nog bestaat, maar u kunt ook kunt u uw toepassingscode toorender toegang beslissingen nadat de App Service Hallo gebruiker is geverifieerd.

Zie voor meer informatie over nieuwe verificatiefuncties Hallo [verificatie en autorisatie voor API-Apps in Azure App Service](app-service-api-authentication.md). Voor informatie over hoe toomigrate bestaande API-apps uit de vorige API-apps Hallo toohello nieuwe één, Zie model [migreren bestaande API apps](#migrating-existing-api-apps) verderop in dit artikel.

### <a name="cors"></a>CORS
In plaats van een door komma's gescheiden **MS_CrossDomainOrigins** app instelt, er wordt een blade hello Azure-beheerportal voor het configureren van CORS. U kunt ook kunnen worden geconfigureerd met Resource Manager tooling zoals Azure PowerShell, CLI of [Resource Explorer](https://resources.azure.com/). Set Hallo **cors** -eigenschap op Hallo **Microsoft.Web/sites/config** resourcetype voor uw  **&lt;sitenaam&gt;/web** resource. Bijvoorbeeld:

    {
        "cors": {
            "allowedOrigins": [
                "https://localhost:44300"
            ]
        }
    } 

### <a name="api-metadata"></a>API-metagegevens
Hallo-API-definitie blade is nu beschikbaar via het Web, mobiel en API-Apps. In de beheerportal hello, kunt u een relatieve url of een absolute url verwijst tooan eindpunt die hosts een Swagger 2.0-representatie van uw API. U kunt ook kunnen worden geconfigureerd met Resource Manager tooling. Set Hallo **apiDefinition** -eigenschap op Hallo **Microsoft.Web/sites/config** resourcetype voor uw  **&lt;sitenaam&gt;/web** resource. Bijvoorbeeld:

    {
        "apiDefinition":
        {
            "url": "https://myStorageAccount.blob.core.windows.net/swagger/apiDefinition.json"
        }
    }

Op dit moment Hallo metagegevenseindpunt moet toobe openbaar toegankelijk zijn zonder verificatie voor veel downstream-clients (bijvoorbeeld Visual Studio REST API client genereren en PowerApps 'API toevoegen' stroom) tooconsume deze. Dit betekent dat als u van App Service-verificatie gebruikmaakt en tooexpose Hallo API-definitie van binnen uw app zelf, moet u toouse Hallo uitgesteld verificatieoptie hierboven worden beschreven, zodat Hallo route tooyour Swagger-metagegevens openbaar is.

## <a name="management-portal"></a>Management Portal
Selecteren **Nieuw > Web + mobiel > API-App** in Hallo portal API-apps die overeenkomen met de nieuwe mogelijkheden hello wordt beschreven in artikel Hallo maakt. **Bladeren > API-Apps** wordt alleen deze nieuwe API-apps. Als u naar een API-app bladeren, Hallo Hallo blade shares dezelfde indeling en mogelijkheden bieden als die van de Web- en mobiele Apps. Hallo alleen verschillen zijn Quick Start-inhoud en ordening van instellingen.

Bestaande API-apps (of Marketplace-API-apps die zijn gemaakt op basis van Logic Apps) Hello vorige Preview-mogelijkheden nog steeds zichtbaar in Hallo Logic Apps designer en bij het bladeren door alle resources in een resourcegroep.

## <a name="visual-studio"></a>Visual Studio
De meeste Web Apps tooling is voor de nieuwe API-apps geschikt omdat ze delen Hallo dezelfde onderliggende **Microsoft.Web/sites** brontype. Hello Azure Visual Studio tooling, moet echter bijgewerkte tooversion 2.8.1 of hoger omdat het wordt een aantal specifieke tooAPIs mogelijkheden. Hallo SDK downloaden van Hallo [pagina Azure downloads](https://azure.microsoft.com/downloads/).

Publiceren met Hallo bedrijfsoptimalisatie Hallo App servicetypen, is ook unified onder **publiceren > Microsoft Azure App Service**:

![API-Apps publiceren](./media/app-service-api-whats-changed/api-apps-publish.png)

meer informatie over de SDK 2.8.1, lees Hallo aankondiging toolearn [blogbericht](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-1-for-net/).

U kunt ook handmatig importeren Hallo publicatieprofiel van Hallo management portal tooenable publiceren. Echter Cloud Explorer, genereren van code en API Apps selectie/maken SDK 2.8.1 vereist of hoger.

## <a name="migrating-existing-api-apps"></a>Migreren van bestaande API-apps
Als uw aangepaste API geïmplementeerde toohello vorige Preview-versie van de API-Apps, vragen wij toohello nieuw model te migreren voor API-Apps met 31 December 2015. Omdat zowel het oude en nieuwe model Hallo zijn gebaseerd op Web-API's die worden gehost in App Service, Hallo meerderheid van de bestaande code opnieuw kan worden gebruikt.

### <a name="hosting-and-redeployment"></a>Host en opnieuw implementeren
stappen voor het distribueren van Hallo zijn hetzelfde als het implementeren van een bestaande Web-API-tooApp Service Hallo. stappen:

1. Maak een lege API-app. Dit is mogelijk in Hallo-portal met New > API-App in Visual Studio van publiceren, of van Resource Manager tooling. Als Resource Manager tooling of sjablonen gebruikt, stelt u Hallo **soort** waarde te**api** op Hallo **Microsoft.Web/sites** resource type toohave Hallo snelstartgidsen en -instellingen in Hallo-beheerportal is gericht op API-scenario's.
2. Verbinding maken en implementeren van uw project toohello leeg API-app met behulp van een Hallo implementatie mechanismen ondersteund door App Service. Lees [documentatie van Azure App Service-implementatie](../app-service-web/web-sites-deploy.md) toolearn meer. 

### <a name="authentication"></a>Authentication
Hallo ondersteuning van App Service-verificatie services Hallo dezelfde mogelijkheden die beschikbaar zijn met de vorige API Apps-model Hallo waren. Als u met behulp van sessie-tokens en SDK's vereisen, gebruikt u Hallo client en server SDK's te volgen:

* Client: [Azure mobiele Client SDK](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/)
* Server: [Microsoft Azure mobiele App .NET-authenticatie-extensie](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/) 

Als u in plaats daarvan Hallo App Service alpha SDK's zijn gebruikt, worden deze nu afgeschafte:

* Client: [AppService-SDK van Microsoft Azure](http://www.nuget.org/packages/Microsoft.Azure.AppService)
* Server: [Microsoft.Azure.AppService.ApiApps.Service](http://www.nuget.org/packages/Microsoft.Azure.AppService.ApiApps.Service)

In het bijzonder met Azure Active Directory is geen App Service-specifieke echter vereist als u de AAD-token Hallo rechtstreeks.

### <a name="internal-access"></a>Interne toegang
Hallo vorige API Apps model een ingebouwde interne toegangsniveau opgenomen. Dit gebruik van Hallo SDK vereist voor het ondertekenen van aanvragen. Zoals eerder beschreven, met de nieuwe API-Apps model hello, kunnen AAD-service-principals worden gebruikt als alternatief voor verificatie van de service to service zonder dat een App Service-specifiek SDK. Meer informatie [principal verificatie van de Service voor API Apps in Azure App Service](app-service-api-dotnet-service-principal-auth.md).

### <a name="discovery"></a>Detectie
Hallo vorige API Apps model had API's voor het detecteren van andere API-apps tijdens runtime in dezelfde resourcegroep achter Hallo Hallo dezelfde gateway. Dit is vooral nuttig in architecturen die microservice patronen te implementeren. Hoewel dit niet rechtstreeks wordt ondersteund, zijn een aantal opties zijn beschikbaar:

1. Hello Azure Resource Manager-API's gebruiken voor detectie.
2. Azure API Management voor uw API-App Service gehost's geplaatst. Azure API Management fungeert als een façade en een stabiele externe gerichte url kunt opgeven, zelfs als u interne topologie verandert.
3. Uw eigen detectie API-app bouwen en andere API-apps registreren bij Hallo detectie app bij het opstarten hebben.
4. Tijdens de implementatie, vul Hallo app-instellingen van alle Hallo API-apps (en clients) Hallo eindpunten Hallo andere API-apps. Dit is beschikbaar in de sjabloon implementaties en de API-Apps kunt u nu besturingselement van het Hallo-url.

## <a name="using-api-apps-with-logic-apps"></a>Met behulp van API-Apps met Logic Apps
nieuw model voor API apps Hallo werkt goed samen met [schemaversie 2015-08-01 van Logic Apps](../logic-apps/logic-apps-schema-2015-08-01.md).

## <a name="next-steps"></a>Volgende stappen
meer lezen Hallo artikelen in Hallo toolearn [API Apps-documentatierubriek](https://azure.microsoft.com/documentation/services/app-service/api/). Ze zijn bijgewerkt tooreflect Hallo nieuw model voor API-Apps. Bovendien bereiken op Hallo-forums voor meer informatie of instructies voor migratie:

* [MSDN-forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureAPIApps)
* [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-api-apps)


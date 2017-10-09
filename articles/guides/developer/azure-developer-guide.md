---
title: aaaGet gestart handleiding voor ontwikkelaars die in Azure | Microsoft Docs
description: "Dit onderwerp bevat essentiële informatie voor ontwikkelaars die op zoek tooget de slag met Microsoft Azure-platform Hallo voor hun ontwikkelingsbehoeften."
services: 
cloud: 
documentationcenter: 
author: ggailey777
manager: erikre
ms.assetid: 
ms.service: na
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: glenga
ms.openlocfilehash: 72dc2678db7738923d4bc7783e297fea6fcded83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-guide-for-azure-developers"></a>Aan de slag-handleiding voor Azure-ontwikkelaars

## <a name="what-is-azure"></a>Wat is Azure?

Azure is een volledig cloud-platform die u kunt uw bestaande toepassingen worden gehost, Hallo ontwikkeling van nieuwe toepassingen te stroomlijnen en on-premises toepassingen zelfs te verbeteren. Azure Hallo cloudservices, moet u toodevelop integreert, testen, implementeren en beheren van uw toepassingen, en tegelijkertijd profiteren van de efficiëntie Hallo van cloud computing.

U kunt uw toepassingen in Azure hosten, begin klein en schaal van uw toepassing eenvoudig omhoog wanneer uw vraag van klanten groeit. Azure biedt ook Hallo betrouwbaarheid die nodig is voor hoge beschikbaarheid-toepassingen, waaronder zelfs failover tussen verschillende regio's. Hallo [Azure-portal](https://portal.azure.com) kunt u eenvoudig alle Azure-services te beheren. U kunt uw services ook programmatisch beheren met behulp van de service-API's en sjablonen.

**Wie dit**: in deze handleiding wordt een toohello inleiding Azure-platform voor toepassingsontwikkelaars. Biedt richtlijnen en moet u toostart bouwen van nieuwe toepassingen in Azure of migreren bestaande toepassingen tooAzure richting.

## <a name="where-do-i-start"></a>Waar moet ik beginnen?

Met alle Hallo-services die Azure biedt, kan een uitdaging taak toofigure welke services u toosupport uw oplossingsarchitectuur moet zijn. Deze sectie licht hello Azure services ontwikkelaars veel gebruiken. Zie voor een lijst met alle Azure-services, Hallo [Azure-documentatie](../../index.md).

Eerst moet u bepalen hoe toohost uw toepassing in Azure. U hoeft toomanage uw volledige infrastructuur als een virtuele machine (VM). Kunt u Hallo platform management faciliteiten die Azure biedt? Mogelijk moet u een zonder server framework toohost code worden uitgevoerd alleen?

Uw toepassing moet cloudopslag, die Azure biedt verschillende opties voor. U kunt profiteren van de enterprise-verificatie van Azure. Er zijn ook hulpprogramma's voor cloud-gebaseerde ontwikkeling en bewaking en de meeste hostingservices DevOps-integratie bieden.

Nu bekijken we enkele specifieke Hallo-services die we aanbevelen voor uw toepassingen onderzoeken.

### <a name="application-hosting"></a>Toepassingen hosten

Azure biedt verschillende cloud-gebaseerde compute aanbiedingen toorun uw toepassing zodat er geen tooworry Hallo infrastructuur details over. U kunt eenvoudig omhoog schalen of uitschalen van uw resources wanneer het toepassingsgebruik van uw groeit.

Azure biedt services die ondersteuning bieden voor uw toepassing ontwikkelen en hosten van behoeften. Azure biedt een infrastructuur-as-a-service (IaaS) toogive u volledige controle over het hosten van uw toepassing. Azure platform as a service (PaaS)-aanbiedingen bieden Hallo volledig beheerd toopower services om uw apps. Er is zelfs true zonder server die als host fungeert in Azure waarop toodo hoeft u uw code te schrijven.

![Azure-toepassing hosting-opties](./media/azure-developer-guide/azure-developer-hosting-options.png)


#### <a name="azure-app-service"></a>Azure App Service 

Als u uw webprojecten Hallo snelste pad toopublish wilt, houd rekening met Azure App Service. App Service kunt u eenvoudig tooextend uw web-apps toosupport uw mobiele clients en eenvoudig verbruikte REST-API's publiceren. Dit platform biedt verificatie via sociale providers, automatisch schalen op basis van verkeer testen in productie en continue en op basis van een container-implementaties.

Wanneer u een app in App Service maken, selecteer een van de volgende typen Hallo:

- [Web-Apps](../../app-service-web/app-service-web-overview.md): kunt hosten van websites en web-apps die zijn geschreven met .NET, Java, PHP, Node.js en Python.

- [Mobile Apps](../../app-service-mobile/app-service-mobile-value-prop.md): breidt Web Apps toosupport toegang vanaf mobiele apparaten. Deze verificatie met sociaalnetwerkproviders en Azure Active Directory (Azure AD) ingeschakeld, biedt back endopslag en kan worden geïntegreerd met [Azure Notification Hubs](../../notification-hubs/notification-hubs-push-notification-overview.md) voor pushmeldingen.

- [API-Apps](../../app-service-api/app-service-api-apps-why-best-platform.md): Hiermee kunt u veilig kunt blootstellen van uw API's in de cloud Hallo met Swagger-metagegevens zodat clients kunnen eenvoudig gebruiken.

Omdat alle drie app-typen delen Hallo App Service-runtime, kunt u een website te hosten, mobiele clients ondersteunen en uw API's in Azure, beschikbaar via Hallo hetzelfde project of oplossing. Zie toolearn meer informatie over App Service [hoe App Service werkt](../../app-service/app-service-how-works-readme.md).

App Service is ontworpen met DevOps in gedachten. Biedt ondersteuning voor verschillende hulpprogramma's voor publiceren en continue integratie implementaties, met inbegrip van GitHub webhooks, Jenkins, Visual Studio Team Services, TeamCity en anderen.

U kunt uw bestaande toepassingen tooApp Service migreren met behulp van Hallo [online Migratiehulpmiddel](https://www.migratetoazure.net/).

>**Wanneer toouse**: App Service gebruiken wanneer u bij het migreren van bestaande tooAzure voor web-toepassingen, en wanneer u een volledig beheerde host-platform hebt voor uw web-apps. U kunt ook een App Service gebruiken als u de REST-API's beschikbaar met uw app of mobiele clients toosupport nodig.

>**Aan de slag**: App Service maakt het eenvoudig toocreate en implementeren van uw eerste [web-app](../../app-service-web/web-sites-dotnet-get-started.md), [mobiele app](../../app-service-mobile/app-service-mobile-ios-get-started.md), of [API-app](../../app-service-api/app-service-api-dotnet-get-started.md).

>**Probeer het nu**: App Service kunt u een eenvoudige app tootry Hallo platform inrichten zonder toosign voor een Azure-account. Probeer het Hallo-platform en [maken van uw app in Azure App Service](https://tryappservice.azure.com/).

#### <a name="azure-virtual-machines"></a>Azure Virtual Machines

Als een infrastructuur-as-a-service (IaaS)-provider, kunt u implementeren met Azure tooor migreren van uw toepassing tooeither Windows of Linux-machines. Samen met Azure Virtual Network ondersteunt Azure Virtual Machines Hallo-implementatie van Windows of Linux-machines tooAzure. Met virtuele machines hebt u volledige controle over Hallo configuratie van Hallo-machine. Wanneer u virtuele machines, bent u verantwoordelijk voor alle software-installatie, configuratie, onderhoud en besturingssysteem patches server.

Vanwege Hallo beheerniveau die u met virtuele machines hebt, kunt u een breed scala aan server-werkbelasting uitvoeren op Azure die niet passen in een PaaS-model. Deze werkbelastingen behoren databaseservers, Windows Server Active Directory en Microsoft SharePoint. Zie voor meer informatie, Hallo virtuele Machines documentatie voor [Linux](/azure/virtual-machines/linux/) of [Windows](/azure/virtual-machines/windows/).

>**Wanneer toouse**: Gebruik virtuele Machines als u wilt dat volledige controle over uw toepassing infrastructuur of toomigrate lokale toepassing werklast tooAzure zonder toomake wijzigingen.

>**Aan de slag**: Maak een [Linux VM](../../virtual-machines/virtual-machines-linux-quick-create-portal.md) of [Windows VM](../../virtual-machines/virtual-machines-windows-hero-tutorial.md) van hello Azure-portal.

#### <a name="azure-functions-serverless"></a>Azure Functions (zonder server)

In plaats van zorgen te hoeven maken over het bouwen van en beheren van een hele toepassing of Hallo infrastructuur toorun uw code. Wat gebeurt er als kan u zojuist hebt uw code te schrijven en uitvoeren in het antwoord tooevents of volgens een schema?  [Azure Functions](../../azure-functions/functions-overview.md) is een 'zonder server'-stijl bieden dat kunt u alleen schrijven Hallo code die je nodig. Met functies, wordt de uitvoering van code geactiveerd door de HTTP-aanvragen, webhooks, cloud servicegebeurtenissen of volgens een schema. U kunt de code in uw taal ontwikkeling keuze, zoals C\#, F\#, Node.js, Python of PHP. U betaalt alleen voor Hallo tijd dat uw code wordt uitgevoerd en Azure schaalt naar behoefte met facturering op basis van verbruik.

>**Wanneer toouse**: gebruik Azure Functions wanneer u code die wordt geactiveerd door een andere Azure-services door gebeurtenissen op basis van een webpagina of volgens een planning hebt. U kunt ook functies gebruiken wanneer u niet nodig Hallo overhead van een volledig gehoste project of als u alleen toopay voor Hallo die uw code wordt uitgevoerd. toolearn meer, Zie [overzicht van Azure Functions](../../azure-functions/functions-overview.md).

>**Aan de slag**: Hallo functies Quick Start-zelfstudie te volgen[maken van uw eerste functie](../../azure-functions/functions-create-first-azure-function.md) van Hallo-portal.

>**Probeer het nu**: Azure Functions, kunt u de code uitvoeren zonder toosign voor een Azure-account. Probeer het nu aan en [uw eerste Azure-functie maken](https://tryappservice.azure.com/).

#### <a name="azure-service-fabric"></a>Azure Service Fabric

Azure Service Fabric is een platform voor gedistribueerde systemen waarmee u eenvoudig toobuild kunt verpakken, implementeren en beheren van schaalbare en betrouwbare microservices. Het bevat ook uitgebreide toepassing beheermogelijkheden voor inrichting, implementatie, bewaking, bijwerken/patchen en verwijderen van toepassingen worden geïmplementeerd. Apps die worden uitgevoerd op een gedeelde groep machines, kunnen begin klein en toohundreds of duizenden computers naar behoefte te schalen.

Service Fabric ondersteunt WebAPI met Open Web Interface voor .NET (OWIN) en ASP.NET Core. Het biedt SDK's voor het bouwen van services op Linux in zowel .NET Core en Java. toolearn meer informatie over Service Fabric Zie Hallo [leertraject voor Service Fabric](https://azure.microsoft.com/documentation/learning-paths/service-fabric/).

>**Wanneer toouse:** Service Fabric is een goede keuze wanneer u een toepassing maken of een bestaande toepassing toouse een microservice-architectuur herschrijven. Service Fabric gebruikt als u meer controle over of directe toegang tot de onderliggende infrastructuur Hallo.

>**Aan de slag:** [uw eerste Azure Service Fabric-toepassing maken](../../service-fabric/service-fabric-create-your-first-application-in-visual-studio.md).

### <a name="enhance-your-applications-with-azure-services"></a>Uw toepassingen met Azure-services te verbeteren

Daarnaast biedt tooapplication hosting van Azure serviceaanbiedingen die Hallo-functionaliteit, ontwikkeling en onderhoud van uw toepassingen, zowel in Hallo cloud en on-premises kunnen verbeteren.

#### <a name="hosted-storage-and-data-access"></a>Gehoste opslag- en -toegang

De meeste toepassingen moet gegevens zo ongeacht van hoe u toohost besluit van uw toepassing in Azure opslaat, overweeg dan een of meer van de Hallo opslag- en -services te volgen.

-   **Azure SQL Database**: een Azure-versie van Microsoft SQL Server-engine voor het opslaan van relationele tabellaire gegevens in de cloud Hallo Hallo. SQL-Database biedt voorspelbare prestaties, schaalbaarheid zonder uitvaltijd, bedrijfscontinuïteit en gegevensbeveiliging.

    >**Wanneer toouse**: wanneer uw toepassing gegevensopslag met referentiële integriteit, transactieondersteuning en ondersteuning vereist voor TSQL-query's.

    >**Aan de slag**: [maken van een SQL-database in minuten met behulp van hello Azure-portal](../../sql-database/sql-database-get-started.md).

-   **Azure Storage**: biedt duurzaam en maximaal beschikbare opslag voor blobs, wachtrijen, bestanden en andere soorten niet-relationele gegevens. Hallo opslag foundation biedt Storage voor virtuele machines.

    >**Wanneer toouse**: wanneer uw app slaat de niet-relationele gegevens, zoals sleutel / waarde-paren (tabellen), blobs, bestanden, shares, of berichten (wachtrijen).

    >**Aan de slag**: Kies een van deze typen opslag: [blobs](../../storage/blobs/storage-dotnet-how-to-use-blobs.md), [tabellen](../../cosmos-db/table-storage-how-to-use-dotnet.md), [wachtrijen](../../storage/queues/storage-dotnet-how-to-use-queues.md), of [bestanden](../../storage/files/storage-dotnet-how-to-use-files.md).

-   **Azure DocumentDB**: een volledig beheerde en schaalbare NoSQL-database-service, die functies van SQL-query's via de objectgegevens. U kunt toegang tot DocumentDB via bestaande stuurprogramma's voor MongoDB.
    >**Wanneer toouse:** wanneer uw toepassing moet toobe kunnen tooexecute SQL-query's via JSON-documenten, of als u MongoDB.

    >**Aan de slag**: [bouwen een DocumentDB C#-consoletoepassing](../../documentdb/documentdb-get-started.md). Als u een ontwikkelaar MongoDB, Zie [DocumentDB protocolondersteuning voor MongoDB](../../documentdb/documentdb-protocol-mongodb.md).

U kunt [Azure Data Factory](../../data-factory/data-factory-introduction.md) toomove bestaande on-premises gegevens tooAzure. Als u niet klaar toomove gegevens toohello cloud [hybride verbindingen](../../biztalk-services/integration-hybrid-connection-overview.md) in BizTalk Services kunt u verbinding maken uw App Service gehost app tooon lokale bronnen. U kunt ook tooAzure gegevens en services verbinden van uw on-premises toepassingen.

#### <a name="docker-support"></a>Docker-ondersteuning

Docker-containers, een vorm van OS virtualisatie, kunnen u toepassingen implementeren op een manier efficiënter en voorspelbare. Een beperkte toepassing werkt in productie Hallo dezelfde manier als op uw systemen ontwikkeling en tests. U kunt de containers beheren met standaard Docker-hulpprogramma's. U kunt uw bestaande vaardigheden en toodeploy van populaire open-source hulpprogramma's gebruiken en beheren van toepassingen op basis van een container in Azure.

Azure biedt verschillende manieren toouse containers in uw toepassingen.

-   **Azure Docker VM-extensie**: Hiermee kunt u uw virtuele machine configureren met Docker extra tooact als Docker-host.

    >**Wanneer toouse**: als u wilt dat de consistente containerimplementaties toogenerate voor uw toepassingen op een virtuele machine of als u wilt dat toouse [Docker Compose](https://docs.docker.com/compose/overview/).

    >**Aan de slag**: [een Docker-omgeving maken in Azure met behulp van Docker VM-extensie voor Hallo](../../virtual-machines/virtual-machines-linux-dockerextension.md).

-   **Azure Container Service**: kunt maken, configureren en beheren van een cluster van virtuele machines die zijn vooraf geconfigureerde toorun beperkte toepassingen. Zie toolearn meer informatie over de Container Service [inleiding Azure Container Service](../../container-service/container-service-intro.md).

    >**Wanneer toouse**: als u toobuild gereed is voor productie, schaalbare omgevingen die extra hulpprogramma's voor planning en beheer bieden, of wanneer u implementeert een Docker Swarm-cluster nodig.

    >**Aan de slag**: [een Container Service-cluster implementeren](../../container-service/dcos-swarm/container-service-deployment.md).

-   **Docker-Machine**: u kunt installeren en beheren van een Docker-Engine op de virtuele hosts met behulp van docker-machine-opdrachten.

    >**Wanneer toouse**: wanneer u tooquickly prototype een app moet door het maken van een afzonderlijke Docker-host.

-   **Aangepaste Docker-installatiekopie voor App Service**: Hiermee kunt u Docker-containers uit het register van een container of een klant-container gebruiken wanneer u een web-app op Linux implementeert.

    >**Wanneer toouse**: bij het implementeren van een web-app op Linux tooa Docker-installatiekopie.

    >**Aan de slag**: [gebruik van een aangepaste Docker-afbeelding voor App-Service op Linux](../../app-service-web/app-service-linux-using-custom-docker-image.md).

### <a name="authentication"></a>Authentication

De cruciale toonot alleen weten wie uw toepassingen, maar ook tooprevent onbevoegde toegang tot tooyour bronnen wordt gebruikt. Azure biedt verschillende manieren tooauthenticate uw app-clients.

-   **Azure Active Directory (Azure AD)**: Hallo Microsoft multitenant, cloud-gebaseerde identiteit en toegang management-service. U kunt eenmalige aanmelding (SSO) tooyour toepassingen toevoegen door te integreren met Azure AD. Eigenschappen van de map is toegankelijk via Azure AD Graph API Hallo rechtstreeks of Hallo Microsoft Graph API. U kunt integreren met Azure AD-ondersteuning voor Hallo OAuth2.0 autorisatie framework en Open ID Connect met behulp van de native HTTP-/ REST-eindpunten en Hallo multiplatform Azure AD-verificatiebibliotheken.

    >**Wanneer toouse**: als u wilt dat tooprovide een SSO-ervaring, werken met gegevens op basis van de grafiek of verificatie van gebruikers op basis van een domein.

    >**Aan de slag**: toolearn meer, Zie Hallo [ontwikkelaarshandleiding Azure Active Directory](../../active-directory/active-directory-developers-guide.md).

-   **Verificatie van App Service**: wanneer u App Service-toohost uw app kiest, u ook ondersteuning voor ingebouwde verificatie voor Azure AD, samen met sociale identiteitsproviders, waaronder Facebook, Google, Microsoft en Twitter.

    >**Wanneer toouse**: als u wilt dat tooenable verificatie in App Service-app met Azure AD sociale identiteitsproviders of beide.

    >**Aan de slag**: toolearn meer informatie over verificatie in App Service, Zie [verificatie en autorisatie in Azure App Service](../../app-service/app-service-authentication-overview.md).

toolearn meer informatie over aanbevolen procedures voor beveiliging in Azure, Zie [Azure-beveiliging aanbevolen procedures en patronen](../../security/security-best-practices-and-patterns.md).

### <a name="monitoring"></a>Bewaking

Uw toepassing binnen Azure, moet u toobe kunnen toomonitor prestaties, Bekijk voor problemen en Zie hoe klanten uw app gebruiken. Azure biedt verschillende opties voor controle.

-   **Visual Studio Application Insights**: een Azure gehoste uitbreidbare Analyseservice die kan worden geïntegreerd met Visual Studio toomonitor uw live-webtoepassingen. Dit biedt u Hallo gegevens dat u nodig hebt toocontinuously Hallo prestaties en bruikbaarheid van uw apps verbeteren, of ze zijn gehost op Azure of niet.

    >**Aan de slag**: Volg Hallo [Application Insights-zelfstudie](../../application-insights/app-insights-overview.md).

-   **Monitor voor Azure**: een service die u helpt toovisualize, query, route, archiveren en act op Hallo metrische gegevens en de logboeken die worden gegenereerd door uw Azure-infrastructuur en de bronnen. Monitor biedt Hallo gegevensweergaven u ziet in hello Azure-portal en één bron voor het bewaken van de Azure-resources is.
 
    >**Aan de slag**: [aan de slag met Azure Monitor](../../monitoring-and-diagnostics/monitoring-get-started.md).

### <a name="devops-integration"></a>Integratie met DevOps

Of het inrichten van virtuele machines of uw web-apps met continue integratie publiceren, Azure kan worden geïntegreerd met de meeste Hallo populaire DevOps-hulpprogramma's. Met ondersteuning voor hulpprogramma's zoals Jenkins, GitHub, Puppet, Chef, TeamCity, Ansible, VSTS en anderen, kunt u werken met hulpprogramma's Hallo dat u al hebt en uw bestaande ervaring te maximaliseren.

>**Probeer het nu:** [uitproberen diverse Hallo DevOps integraties](https://azure.microsoft.com/try/devops/).

>**Aan de slag**: toosee DevOps-opties voor een App Service-app, Zie [continue implementatie tooAzure App Service](../../app-service-web/app-service-continuous-deployment.md).


## <a name="azure-regions"></a>Azure-regio's

Azure is een globale cloudplatform die algemeen beschikbaar is in veel regio Hallo wereld. Wanneer u een service, toepassing of virtuele machine in Azure inricht, bent u tooselect gevraagd een regio, wat staat voor een specifieke datacenter waarin de toepassing wordt uitgevoerd of waar uw gegevens worden opgeslagen. Deze gebieden overeen toospecific locaties die worden gepubliceerd op Hallo [Azure-regio's](https://azure.microsoft.com/regions/) pagina.

### <a name="choose-hello-best-region-for-your-application-and-data"></a>Kies de beste regio Hallo voor uw toepassing en gegevens

Een van de voordelen van het gebruik van Azure Hallo is dat u uw toepassingen toovarious datacenters hele Hallo wereld kunt implementeren. Hallo regio die u kiest, kan Hallo-prestaties van uw toepassing beïnvloeden. Bijvoorbeeld, is het beter toochoose een regio die het dichter toomost van uw klanten tooreduce latentie in netwerkaanvragen. U kunt uw regio toomeet Hallo wettelijke vereisten voor het distribueren van uw app in bepaalde landen ook tooselect. Het is altijd een best practice toostore toepassingsgegevens hetzelfde datacenter Hallo of in een datacenter zo dicht als mogelijke toohello datacenter dat als host fungeert voor uw toepassing.

### <a name="multi-region-apps"></a>Meerdere landen/regio-apps

Hoewel onwaarschijnlijk, is het niet onmogelijk voor een hele datacenter toogo offline vanwege een gebeurtenis, zoals een natuurramp of Internet-fout. Het is een best practice toohost essentiële business-toepassingen in meer dan één datacenter tooprovide maximale beschikbaarheid. Met behulp van meerdere regio's kan ook de latentie voor globale gebruikers te verminderen en bieden meer mogelijkheden voor flexibiliteit bij het bijwerken van toepassingen.

Sommige services, zoals virtuele Machine en App-Services, gebruik [Azure Traffic Manager](../../traffic-manager/traffic-manager-overview.md) tooenable meerdere landen/regio ondersteuning met failover tussen regio's toosupport hoge beschikbaarheid bedrijfstoepassingen. Zie voor een voorbeeld [naslaginformatie over Azure-architectuur: webtoepassing met hoge beschikbaarheid](../../guidance/guidance-web-apps-multi-region.md).

>**Wanneer toouse**: wanneer u een enterprise- en hoge beschikbaarheid toepassingen die van failover- en replicatie profiteren hebt.

## <a name="how-do-i-manage-my-applications-and-projects"></a>Hoe beheer ik mijn toepassingen en projecten?

Azure biedt een uitgebreide set ervaringen voor u toocreate en beheren van uw Azure-resources, toepassingen en projecten: zowel programmatisch als in Hallo [Azure-portal](https://portal.azure.com/).

### <a name="command-line-interfaces-and-powershell"></a>Opdrachtregelinterfaces en PowerShell

Azure biedt twee manieren toomanage uw toepassingen en services vanaf de opdrachtregel Hallo via Bash, Terminal, Hallo-opdrachtprompt of het opdrachtregelhulpprogramma van keuze. Meestal kunt u dezelfde taken Hallo uitvoeren vanaf de opdrachtregel Hallo zoals hello Azure-portal in, zoals het maken en configureren van virtuele machines, virtuele netwerken, web-apps en andere services.

-   [Azure-opdrachtregelinterface (CLI)](../../xplat-cli-install.md): Hiermee kunt u verbinding tooan Azure-abonnement en diverse taken op basis van de Azure-resources vanaf de opdrachtregel Hallo programma.

-   [Azure PowerShell](../../powershell-install-configure.md): biedt een set modules met cmdlets waarmee u toomanage Azure resources met behulp van Windows PowerShell.

### <a name="azure-portal"></a>Azure Portal

Hello Azure-portal is een webtoepassing die u kunt toocreate gebruiken, beheren en Azure-resources en services verwijderen. Hello Azure-portal bevindt zich op <https://portal.azure.com>. Het bevat een aangepast dashboard, hulpprogramma's voor het beheren van Azure-resources en toosubscription toegangsinstellingen en factureringsgegevens. Zie voor meer informatie, Hallo [overzicht van Azure portal](../../azure-portal-overview.md).

### <a name="rest-apis"></a>REST-API’s

Azure is gebouwd op een set REST-API's die ondersteuning bieden voor Hallo gebruikersinterface van Azure portal. De meeste van deze REST-API's zijn ook ondersteunde toolet u programmatisch inrichten en beheren van uw Azure-resources en toepassingen vanaf elk apparaat toegang tot Internet hebben. Zie voor de volledige set Hallo van REST-API-documentatie, Hallo [REST-SDK van Azure verwijzing](https://docs.microsoft.com/rest/api/).

### <a name="apis"></a>API's

Bovendien tooREST API's, vele Azure-services ook kunnen u resources van uw toepassingen programmatisch te beheren met behulp van de platform-specifieke Azure SDK's, met inbegrip van SDK's voor Hallo ontwikkelplatforms te volgen:

-   [.NET](https://go.microsoft.com/fwlink/?linkid=834925)
-   [Node.js](http://azure.github.io/azure-sdk-for-node/)
-   [Java](https://docs.microsoft.com/java/api/)
-   [PHP](https://github.com/Azure/azure-sdk-for-php/blob/master/README.md)
-   [Python](http://azure-sdk-for-python.readthedocs.io/en/latest/)
-   [Ruby](https://github.com/Azure/azure-sdk-for-ruby/blob/master/README.md)

Services, zoals [Mobile Apps](../../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md) en [Azure Media Services](../../media-services/media-services-dotnet-how-to-use.md) toolet voor clientzijde-SDK's bieden u toegang tot services van web- en voor mobiele ClientApps.

### <a name="azure-resource-manager"></a>Azure Resource Manager 
    
Uw app uitgevoerd op Azure waarschijnlijk te maken met meerdere Azure-services, alle cyclus van welke Volg dezelfde levenscyclus Hallo en kunnen worden beschouwd als een logische eenheid. Een web-app kan bijvoorbeeld Web-Apps, SQL-Database, opslag, Azure Redis-Cache en Azure Content Delivery Network services gebruiken. [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) kunt u met Hallo resources in uw toepassing als groep werken. U kunt implementeren, bijwerken of verwijderen van alle Hallo resources in een enkele, gecoördineerde bewerking.

Bovendien toologically groeperen en beheren van verwante resources, Azure Resource Manager bevat implementatiemogelijkheden waarmee u het Hallo-implementatie en configuratie van gerelateerde resources aanpassen. U kunt met Resource Manager, bijvoorbeeld, implementeren en configureren van een toepassing die uit meerdere virtuele machines, een load balancer en een Azure SQL database als één eenheid bestaat.

U kunt deze implementaties ontwikkelen met behulp van een Azure Resource Manager-sjabloon een document JSON-indeling is. Sjablonen kunt u een implementatie definiëren en beheren van uw toepassingen met behulp van declaratieve sjablonen, in plaats van scripts. De sjablonen kunnen werken voor verschillende omgevingen, zoals testen, Faseren en productie. U kunt bijvoorbeeld een knop tooa GitHub-repo die Hallo-code in Hallo opslagplaats tooa set met Azure-services met één klik implementeert toevoegen met behulp van sjablonen.

>**Wanneer toouse**: gebruik Resource Manager-sjablonen als u wilt dat een implementatie op basis van een sjabloon voor uw app die u programmatisch beheren kunt met behulp van REST-API's hello Azure CLI en Azure PowerShell.

>**Aan de slag**: tooget gestart met behulp van sjablonen Zie [Azure Resource Manager-sjablonen samenstellen](../../resource-group-authoring-templates.md).

## <a name="understanding-accounts-subscriptions-and-billing"></a>Wat zijn accounts, abonnementen en facturering

Ontwikkelaars, we toodive, zoals in Hallo code en probeer het tooget gestart zo snel mogelijk bij het maken van onze toepassingen worden uitgevoerd. Willen we zeker tooencourage toostart u net zo eenvoudig mogelijk in Azure AD werkt. toohelp maken het gemakkelijk, Azure biedt een [gratis proefversie](https://azure.microsoft.com/free/). Sommige services zelfs een 'Gratis proberen'-functionaliteit hebben, zoals [Azure App Service](https://tryappservice.azure.com/), niet waarvoor u een account zelfs te maken. Als plezier omdat deze toodive in coderen en implementeren van uw toepassing tooAzure, het is ook belangrijk tootake enige tijd toounderstand de werking van Azure uit oogpunt van gebruikersaccounts, abonnementen en facturering.

### <a name="what-is-an-azure-account"></a>Wat is een Azure-account?

toobe kunnen toocreate of werken met een Azure-abonnement, moet u een Azure-account hebben. Een Azure-account is gewoon een identiteit in Azure AD of in een map, zoals de organisatie van een werk- of schoolaccount, die wordt vertrouwd door Azure AD. Als u niet deel uit van een organisatie toosuch, kunt u altijd een abonnement maken met behulp van uw Microsoft-Account wordt vertrouwd door Azure AD. toolearn meer informatie over het lokale Windows Server Active Directory integreren met Azure AD, Zie [uw on-premises identiteiten integreren met Azure Active Directory](../../active-directory/active-directory-aadconnect.md).

Voor elk Azure-abonnement is er een vertrouwensrelatie met een Azure AD-exemplaar. Dit betekent dat dat tooauthenticate directory wordt vertrouwd gebruikers, services en apparaten. Meerdere abonnementen kunnen vertrouwen, Hallo dezelfde map, maar een abonnement vertrouwt slechts één directory. toolearn meer, Zie [hoe Azure-abonnementen worden gekoppeld aan Azure Active Directory](../../active-directory/active-directory-how-subscriptions-associated-directory.md).

Bovendien toodefining afzonderlijke Azure-account-id's, ook wel *gebruikers*, kunt u definiëren *groepen* in Azure AD. Gebruikersgroepen maken, is een uitstekende manier toomanage toegang tooresources in een abonnement met behulp van op rollen gebaseerde toegangsbeheer (RBAC). hoe toocreate groepen, Zie toolearn [een groep maken in Azure Active Directory-preview](../../active-directory/active-directory-groups-create-azure-portal.md). U kunt ook groepen maken en beheren door [met behulp van PowerShell](../../active-directory/active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

### <a name="manage-your-subscriptions"></a>Uw abonnementen beheren

Een abonnement is een logische eenheid van Azure-services die gekoppelde tooan Azure-account. Elke gekoppelde account heeft een rol in een abonnement. Facturering voor Azure-services wordt uitgevoerd op basis van per abonnement. Zie voor een lijst van Hallo beschikbaar abonnement aanbiedingen door type [Details van Microsoft Azure-aanbieding](https://azure.microsoft.com/support/legal/offer-details/).

#### <a name="administrator-roles"></a>Beheerdersrollen

Een Azure-abonnement heeft meerdere account administratorrollen die u op elk gewenst moment kunt toewijzen.

-   **Accountbeheerder**: deze rol heeft volledige controle over Hallo-abonnement en Hallo-account dat verantwoordelijk is voor facturering.

-   **Servicebeheerder**: deze rol heeft controle over alle Hallo-services in het Hallo-abonnement. Dit is standaard Hallo hetzelfde account als accountbeheerder Hallo.

-   **Medebeheerder**: deze rol heeft Hallo dezelfde toegang als Hallo-servicebeheerder, behalve dat het Hallo-koppeling van Hallo abonnement tooan Azure-map niet wijzigen.

toolearn meer informatie over beheerdersrollen, Zie [hoe tooadd of wijzig Azure-beheerdersrollen](../../billing/billing-add-change-azure-subscription-administrator.md#add-an-admin-for-a-subscription).

#### <a name="resource-groups"></a>Resourcegroepen

Wanneer u een nieuwe Azure-services inricht, kunt u dit doen in een bepaald abonnement. Afzonderlijke Azure-services, ook wel resources genoemd, worden gemaakt in de context van een resourcegroep Hallo. Resourcegroepen maken het gemakkelijker toodeploy resources en beheren van uw toepassing. Een resourcegroep moet alle Hallo resources voor uw toepassing die u toowork met als eenheid wilt bevatten. U kunt resources verplaatsen tussen resourcegroepen en zelfs toodifferent abonnementen. toolearn over het verplaatsen van resources, Zie [verplaatsen van resources toonew resourcegroep of abonnement](../../resource-group-move-resources.md).

Hello Azure Resource Explorer is een uitstekend hulpprogramma voor het visualiseren van Hallo-resources die u al hebt gemaakt in uw abonnement. toolearn meer, Zie [tooview Azure Resource Explorer gebruiken en het wijzigen van resources](../../resource-manager-resource-explorer.md).

#### <a name="grant-access-tooresources"></a>Verleen toegang tooresources

Als u toegang tooAzure resources toestaat, maar het is altijd een best practice om gebruikers met Hallo minimale bevoegdheden die vereiste tooperform een bepaalde taak.

-   **Op rollen gebaseerde toegangsbeheer (RBAC)**: In Azure, kunt u toegang verlenen toouser accounts (principals) bij een opgegeven bereik: abonnement, resourcegroep of afzonderlijke resources. RBAC kunt u een set resources implementeren in een resourcegroep en verleen machtigingen tooa specifieke gebruiker of groep. Ook kunt u toegang tot tooonly Hallo bronnen die deel uitmaken van de doelresourcegroep toohello beperken. U kunt ook toegang tooa één resource, zoals een virtuele machine of een virtueel netwerk verlenen. toegang tot toogrant, die u toewijst een rol toohello gebruiker, groep of service-principal. Er zijn veel vooraf gedefinieerde rollen en u kunt ook uw eigen aangepaste rollen definiëren.

    >**Wanneer toouse**: wanneer u Geavanceerd toegangsbeheer voor gebruikers en groepen nodig.

    >**Aan de slag**: toolearn meer, Zie [aan de slag met toegangsbeheer in Azure-portal Hallo](../../active-directory/role-based-access-control-what-is.md).

-   **Service-principals**: bovendien tooproviding toouser principals en groepen openen, verleent u Hallo dezelfde toegang tooa service-principal.

    > **Wanneer toouse**: wanneer u programmatisch beheer van Azure-resources of verlenen van toegang voor toepassingen. Zie voor meer informatie [supplication van een Active Directory en service-principal](../../resource-group-create-service-principal-portal.md).

#### <a name="tags"></a>Tags

Azure Resource Manager kunt u aangepaste labels tooindividual bronnen toewijzen. Labels die sleutel-waardeparen, kunnen nuttig zijn wanneer u tooorganize bronnen nodig voor facturering of bewaken. Tags bieden een manier tootrack resources via meerdere resourcegroepen. U kunt de labels in Hallo-portal in hello Azure Resource Manager-sjabloon of programmatisch met behulp van Hallo REST-API, hello Azure CLI of PowerShell kunt toewijzen. U kunt meerdere labels tooeach resource toewijzen. toolearn meer, Zie [Using tags tooorganize uw Azure-resources](../../resource-group-using-tags.md).

### <a name="billing"></a>Facturering

Zijn belangrijke problemen in Hallo verplaatsen van on-premises computing toocloud gehoste services, schatten gebruik van de service en gerelateerde kosten en bij te houden. Het is belangrijk toobe kunnen tooestimate welke nieuwe resources toorun op basis van de maandelijkse kosten. U moet ook toobe kunnen tooproject hoe Hallo facturering voor een bepaalde maand op basis van het huidige uitgaven Hallo eruit ziet.

#### <a name="get-resource-usage-data"></a>Gegevens over brongebruik ophalen

Azure biedt een reeks facturering REST-API's waarmee toegang tooresource gebruiks- en metagegevensinformatie voor de Azure-abonnementen. Deze facturering API's kunt u de mogelijkheid toobetter Hallo voorspellen en Azure kosten beheren. U kunt bijhouden en analyseren uitgaven in perioden van een uur, bestedingslimiet waarschuwingen maken en voorspellen van toekomstige facturering op basis van huidige trends in gebruik.

>**Aan de slag**: toolearn meer over het gebruik van Hallo facturering API's, Zie [overzicht van Azure-facturering gebruik en RateCard APIs](../../billing-usage-rate-card-overview.md).

#### <a name="predict-future-costs"></a>Voorspellen van toekomstige kosten

Hoewel het moeilijk is tooestimate kosten tevoren, Azure heeft een [prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/calculator/) resources die u gebruiken kunt wanneer u een schatting maken van Hallo kosten van geïmplementeerd. U kunt ook Hallo facturering blade in Hallo-portal en Hallo REST-API's facturering tooestimate toekomstige kosten, op basis van huidige verbruik.

>**Aan de slag**: Zie [overzicht van Azure-facturering gebruik en RateCard APIs](../../billing-usage-rate-card-overview.md).

#### <a name="set-up-billing-alerts"></a>Meldingen voor facturering instellen

Nadat u uw toepassing of oplossing op Azure hebt geïmplementeerd, kunt u waarschuwingen die u bij het benaderen van Hallo bestedingslimieten die zijn gedefinieerd in de waarschuwing Hallo e verzenden.

>**Aan de slag**: toolearn meer, Zie [waarschuwingen voor uw Microsoft Azure-abonnementen facturering instellen](../../billing-set-up-alerts.md).

---
title: Mobile Apps in Azure App Service
description: Lees welke voordelen App Service heeft voor de mobiele apps in uw onderneming.
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: 4e96cb9d-a632-4cf6-8219-0810d8ade3f9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ac35ff9fe1c5f315c4de08de951f505627ec412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <span data-ttu-id="331d9-103"><a name="getting-started"> </a>Mobile Apps in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="331d9-103"><a name="getting-started"> </a>About Mobile Apps in Azure App Service</span></span>
<span data-ttu-id="331d9-104">Azure App Service is een volledig beheerde [PaaS-](https://azure.microsoft.com/overview/what-is-paas/)aanbieding (Platform as a Service) voor professionele ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="331d9-104">Azure App Service is a fully managed [platform as a service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) offering for professional developers.</span></span> <span data-ttu-id="331d9-105">De service biedt een uitgebreide reeks mogelijkheden voor web-, mobiele en integratiescenario's.</span><span class="sxs-lookup"><span data-stu-id="331d9-105">The service brings a rich set of capabilities to web, mobile, and integration scenarios.</span></span> 

<span data-ttu-id="331d9-106">De functie Mobile Apps in Azure App Service is een zeer schaalbaar, wereldwijd beschikbaar platform waarmee ontwikkelaars in zakelijke ondernemingen en systeemintegrators mobiele toepassingen kunnen ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="331d9-106">The Mobile Apps feature of Azure App Service gives enterprise developers and system integrators a mobile-application development platform that's highly scalable and globally available.</span></span>

![Visueel overzicht van de mogelijkheden van Mobile Apps](./media/app-service-mobile-value-prop/overview.png)

## <a name="why-mobile-apps"></a><span data-ttu-id="331d9-108">Waarom Mobile Apps?</span><span class="sxs-lookup"><span data-stu-id="331d9-108">Why Mobile Apps?</span></span>
<span data-ttu-id="331d9-109">Met de functie Mobile Apps kunt u het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="331d9-109">With the Mobile Apps feature, you can:</span></span>

* <span data-ttu-id="331d9-110">**Native en platformoverschrijdende apps bouwen**: of u nu native iOS-, Android- of Windows-apps, of platformoverschrijdende Xamarin- of Cordova-apps (Phonegap) bouwt, u hebt altijd voordeel van App Service door native SDK's te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="331d9-110">**Build native and cross-platform apps**: Whether you're building native iOS, Android, and Windows apps or cross-platform Xamarin or Cordova (PhoneGap) apps, you can take advantage of App Service by using native SDKs.</span></span>
* <span data-ttu-id="331d9-111">**Verbinding maken met uw bedrijfssystemen**: met de functie Mobile Apps kunt u in slechts enkele minuten zakelijke aanmeldingen toevoegen en verbinding maken met uw bedrijfsresources, on-premises of in de cloud.</span><span class="sxs-lookup"><span data-stu-id="331d9-111">**Connect to your enterprise systems**: With the Mobile Apps feature, you can add corporate sign-in in minutes, and connect to your enterprise on-premises or cloud resources.</span></span>
* <span data-ttu-id="331d9-112">**Apps bouwen die offline beschikbaar zijn met gegevenssynchronisatie**: maak uw mobiele werknemers productiever door apps te bouwen die offline werken en door gebruik te maken van Mobile Apps om gegevens op de achtergrond te synchroniseren wanneer er verbinding is met een van uw gegevensbronnen of SaaS-API's (Software as a Service) in de onderneming.</span><span class="sxs-lookup"><span data-stu-id="331d9-112">**Build offline-ready apps with data sync**: Make your mobile workforce more productive by building apps that work offline, and use Mobile Apps to sync data in the background when connectivity is present with any of your enterprise data sources or software as a service (SaaS) APIs.</span></span>
* <span data-ttu-id="331d9-113">**Pushmeldingen in enkele seconden naar miljoenen klanten verzenden**: houd contact met uw klanten door gebruik te maken van directe pushmeldingen op elk apparaat, afgestemd op de eigen behoeften van de klant en verzonden op het gewenste moment.</span><span class="sxs-lookup"><span data-stu-id="331d9-113">**Push notifications to millions in seconds**: Engage your customers with instant push notifications on any device, personalized to their needs and sent when the time is right.</span></span>

## <a name="mobile-apps-features"></a><span data-ttu-id="331d9-114">Functies van Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="331d9-114">Mobile Apps features</span></span>
<span data-ttu-id="331d9-115">De volgende functies zijn belangrijk wanneer u mobiele apps ontwikkelt die zijn ingeschakeld voor de cloud:</span><span class="sxs-lookup"><span data-stu-id="331d9-115">The following features are important to cloud-enabled mobile development:</span></span>

* <span data-ttu-id="331d9-116">**Verificatie en autorisatie**: u kunt kiezen uit een steeds groeiende lijst met id-providers, zoals Azure Active Directory, voor ondernemingsverificatie, plus providers van sociale netwerken, zoals Facebook-, Google-, Twitter- en Microsoft-accounts.</span><span class="sxs-lookup"><span data-stu-id="331d9-116">**Authentication and authorization**: Select from an ever-growing list of identity providers, including Azure Active Directory for enterprise authentication, plus social providers such as Facebook, Google, Twitter, and Microsoft accounts.</span></span> <span data-ttu-id="331d9-117">Mobile Apps biedt een OAuth 2.0-service voor elke provider.</span><span class="sxs-lookup"><span data-stu-id="331d9-117">Mobile Apps offers an OAuth 2.0 service for each provider.</span></span> <span data-ttu-id="331d9-118">Daarnaast kunt u de SDK voor de id-provider ook integreren voor providerspecifieke functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="331d9-118">You can also integrate the SDK for the identity provider for provider-specific functionality.</span></span>

    <span data-ttu-id="331d9-119">Lees meer over onze [verificatiefuncties].</span><span class="sxs-lookup"><span data-stu-id="331d9-119">Discover more about our [authentication features].</span></span>

* <span data-ttu-id="331d9-120">**Gegevenstoegang**: Mobile Apps biedt een voor mobiele apparaten geschikte OData v3-gegevensbron die is gekoppeld aan Azure SQL Database of een on-premises SQL-server.</span><span class="sxs-lookup"><span data-stu-id="331d9-120">**Data access**: Mobile Apps provides a mobile-friendly OData v3 data source that's linked to Azure SQL Database or an on-premises SQL server.</span></span> <span data-ttu-id="331d9-121">Omdat deze service kan worden gebaseerd op Entity Framework, kunt u eenvoudig integreren met andere NoSQL- en SQL-gegevensproviders, zoals [Azure Table Storage], MongoDB, [Azure Cosmos DB] en SaaS API-providers zoals Office 365 en Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="331d9-121">Because this service can be based on Entity Framework, you can easily integrate with other NoSQL and SQL data providers, including [Azure Table storage], MongoDB, [Azure Cosmos DB], and SaaS API providers such as Office 365 and Salesforce.com.</span></span>

* <span data-ttu-id="331d9-122">**Offlinesynchronisatie**: met behulp van onze client-SDK's kunt u eenvoudig robuuste en responsieve mobiele toepassingen ontwikkelen die met een offline-gegevensset werken.</span><span class="sxs-lookup"><span data-stu-id="331d9-122">**Offline sync**: Our client SDKs make it easy to build robust and responsive mobile applications that operate with an offline dataset.</span></span> <span data-ttu-id="331d9-123">U kunt deze gegevensset automatisch met de gegevens in de back-end synchroniseren en er is ook ondersteuning voor conflictoplossing.</span><span class="sxs-lookup"><span data-stu-id="331d9-123">You can sync this dataset automatically with the back-end data, including conflict-resolution support.</span></span>

  <span data-ttu-id="331d9-124">Lees meer over onze [gegevensfuncties].</span><span class="sxs-lookup"><span data-stu-id="331d9-124">Discover more about our [data features].</span></span>

* <span data-ttu-id="331d9-125">**Pushmeldingen**: onze client-SDK's kunnen probleemloos worden geïntegreerd met de registratiemogelijkheden van Azure Notification Hubs, zodat u pushmeldingen naar miljoenen gebruikers tegelijk kunt verzenden.</span><span class="sxs-lookup"><span data-stu-id="331d9-125">**Push notifications**: Our client SDKs integrate seamlessly with the registration capabilities of Azure Notification Hubs, so you can send push notifications to millions of users simultaneously.</span></span>

  <span data-ttu-id="331d9-126">Lees meer over onze [functies voor pushmeldingen].</span><span class="sxs-lookup"><span data-stu-id="331d9-126">Discover more about our [push notification features].</span></span>

* <span data-ttu-id="331d9-127">**Client-SDK's**: wij bieden een volledige set client-SDK's voor native ontwikkeling ([iOS], [Android] en [Windows]), platformoverschrijdende ontwikkeling ([Xamarin.iOS en Xamarin.Android], [Xamarin.Forms]) en hybride toepassingsontwikkeling ([Apache Cordova]).</span><span class="sxs-lookup"><span data-stu-id="331d9-127">**Client SDKs**: We provide a complete set of client SDKs that cover native development ([iOS], [Android], and [Windows]), cross-platform development ([Xamarin.iOS and Xamarin.Android], [Xamarin.Forms]), and hybrid application development ([Apache Cordova]).</span></span> <span data-ttu-id="331d9-128">Elke client-SDK is beschikbaar met een MIT-licentie en is open source.</span><span class="sxs-lookup"><span data-stu-id="331d9-128">Each client SDK is available with an MIT license and is open source.</span></span>

## <a name="azure-app-service-features"></a><span data-ttu-id="331d9-129">Functies van Azure App Service</span><span class="sxs-lookup"><span data-stu-id="331d9-129">Azure App Service features</span></span>
<span data-ttu-id="331d9-130">De volgende platformfuncties zijn handig voor mobiele productiesites:</span><span class="sxs-lookup"><span data-stu-id="331d9-130">The following platform features are useful for mobile production sites:</span></span>

* <span data-ttu-id="331d9-131">**Automatische schaling**: met App Service kunt u snel omhoog of uitschalen om in te spelen op de inkomende belasting van klanten.</span><span class="sxs-lookup"><span data-stu-id="331d9-131">**Autoscaling**: With App Service, you can quickly scale up or scale out to handle any incoming customer load.</span></span> <span data-ttu-id="331d9-132">U kunt handmatig het aantal VM's en de grootte ervan selecteren of automatische schaling instellen, zodat de back-end voor uw mobiele app wordt geschaald op basis van uw belasting of schema.</span><span class="sxs-lookup"><span data-stu-id="331d9-132">Manually select the number and size of VMs, or set up autoscaling to scale your mobile-app back end based on load or schedule.</span></span>

  <span data-ttu-id="331d9-133">Lees meer over [Automatische schaling].</span><span class="sxs-lookup"><span data-stu-id="331d9-133">Discover more about [autoscaling].</span></span>

* <span data-ttu-id="331d9-134">**Faseringsomgevingen**: met App Service kunt u meerdere versies van uw site uitvoeren, zodat u A/B-tests, tests in de productieomgeving als onderdeel van een groter DevOps-plan en in-place fasering van een nieuwe back-end kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="331d9-134">**Staging environments**: App Service can run multiple versions of your site, so you can perform A/B testing, test in production as part of a larger DevOps plan, and do in-place staging of a new back end.</span></span>

  <span data-ttu-id="331d9-135">Lees meer over [Faseringsomgevingen].</span><span class="sxs-lookup"><span data-stu-id="331d9-135">Discover more about [staging environments].</span></span>

* <span data-ttu-id="331d9-136">**Doorlopende implementatie**: App Service kan worden geïntegreerd met veelgebruikte SCM-systemen (Supply Chain Management), zodat u automatisch een nieuwe versie van uw back-end kunt implementeren door een vertakking van uw SCM-systeem te pushen.</span><span class="sxs-lookup"><span data-stu-id="331d9-136">**Continuous deployment**: App Service can integrate with common supply chain management (SCM) systems, so you can automatically deploy a new version of your back end by pushing to a branch of your SCM system.</span></span>

  <span data-ttu-id="331d9-137">Lees meer over [implementatieopties].</span><span class="sxs-lookup"><span data-stu-id="331d9-137">Discover more about [deployment options].</span></span>

* <span data-ttu-id="331d9-138">**Virtuele netwerken**: App Service kan verbinding maken met on-premises resources met behulp van een virtueel netwerk, Azure ExpressRoute of hybride verbindingen.</span><span class="sxs-lookup"><span data-stu-id="331d9-138">**Virtual networking**: App Service can connect to on-premises resources by using virtual network, Azure ExpressRoute, or hybrid connections.</span></span>

  <span data-ttu-id="331d9-139">Lees meer over [hybride verbindingen], [virtuele netwerken] en [ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="331d9-139">Discover more about [hybrid connections], [virtual networks], and [ExpressRoute].</span></span>

* <span data-ttu-id="331d9-140">**Geïsoleerde/toegewezen omgevingen**: u kunt App Service uitvoeren in een volledig geïsoleerde en toegewezen omgeving, zodat Azure App Service-apps veilig en op grote schaal kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="331d9-140">**Isolated and dedicated environments**: You can run App Service in a fully isolated and dedicated environment for securely running Azure App Service apps at high scale.</span></span> <span data-ttu-id="331d9-141">Deze omgeving is ideaal voor toepassingsworkloads die op grote schaal worden uitgevoerd, of waarvoor isolatie of beveiligde netwerktoegang nodig is.</span><span class="sxs-lookup"><span data-stu-id="331d9-141">This environment is ideal for application workloads that require high scale, isolation, or secure network access.</span></span>

  <span data-ttu-id="331d9-142">Lees meer over [App Service-omgevingen].</span><span class="sxs-lookup"><span data-stu-id="331d9-142">Discover more about [App Service environments].</span></span>

## <a name="next-steps"></a><span data-ttu-id="331d9-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="331d9-143">Next steps</span></span>

<span data-ttu-id="331d9-144">Begin met de zelfstudie [Aan de slag] om snel bekend te raken met Mobile Apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="331d9-144">To get started with Mobile Apps in Azure App Service, complete the [getting started] tutorial.</span></span> <span data-ttu-id="331d9-145">De zelfstudie bevat de basisinformatie voor het produceren van een mobiele back-end en een client van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="331d9-145">The tutorial covers the basics of producing a mobile back end and client of your choice.</span></span> <span data-ttu-id="331d9-146">Er wordt ook aandacht besteed aan het integreren van verificatie, offlinesynchronisatie en pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="331d9-146">It also covers integrating authentication, offline sync, and push notifications.</span></span> <span data-ttu-id="331d9-147">U kunt de zelfstudie meerdere keren volgen, steeds voor een andere clienttoepassing.</span><span class="sxs-lookup"><span data-stu-id="331d9-147">You can complete the tutorial multiple times, once for each client application.</span></span>

<span data-ttu-id="331d9-148">Zie ons [leeroverzicht] voor meer informatie over Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="331d9-148">For more information about Mobile Apps, review our [learning map].</span></span>
<span data-ttu-id="331d9-149">Zie [Azure App Service] voor meer informatie over het Azure App Service-platform.</span><span class="sxs-lookup"><span data-stu-id="331d9-149">For more information about the Azure App Service platform, see [Azure App Service].</span></span>

<!-- URLs. -->
[Migrate your mobile service to App Service]: app-service-mobile-migrating-from-mobile-services.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[Aan de slag]: app-service-mobile-ios-get-started.md
[Azure Table Storage]:../cosmos-db/table-storage-how-to-use-dotnet.md
[Azure Cosmos DB]: ../cosmos-db/documentdb-get-started.md
[verificatiefuncties]: ./app-service-mobile-auth.md
[gegevensfuncties]: ./app-service-mobile-offline-data-sync.md
[functies voor pushmeldingen]: ../notification-hubs/notification-hubs-push-notification-overview.md
[iOS]: ./app-service-mobile-ios-how-to-use-client-library.md
[Android]: ./app-service-mobile-android-how-to-use-client-library.md
[Windows]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.iOS en Xamarin.Android]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.Forms]: ./app-service-mobile-xamarin-forms-get-started.md
[Apache Cordova]: ./app-service-mobile-cordova-how-to-use-client-library.md
[Automatische schaling]: ../app-service-web/web-sites-scale.md
[Faseringsomgevingen]: ../app-service-web/web-sites-staged-publishing.md
[implementatieopties]: ../app-service-web/web-sites-deploy.md
[hybride verbindingen]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[virtuele netwerken]: ../app-service-web/web-sites-integrate-with-vnet.md
[ExpressRoute]: ../app-service-web/app-service-app-service-environment-network-configuration-expressroute.md
[App Service-omgevingen]: ../app-service-web/app-service-app-service-environment-intro.md
[leeroverzicht]: https://azure.microsoft.com/en-us/documentation/learning-paths/appservice-mobileapps/

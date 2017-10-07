---
title: aaaGeo omsloten pushmeldingen met Azure Notification Hubs en ruimtelijke Bing-gegevens | Microsoft Docs
description: In deze zelfstudie leert u hoe toodeliver op basis van locatie-pushmeldingen met Azure Notification Hubs en ruimtelijke Bing-gegevens.
services: notification-hubs
documentationcenter: windows
keywords: pushmelding,pushmelding
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: d6efe473537f2159240c53e780741f12619c045d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="5bcfd-104">Pushmeldingen met geofencing verzenden met Azure Notification Hubs en ruimtelijke Bing-gegevens</span><span class="sxs-lookup"><span data-stu-id="5bcfd-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="5bcfd-105">toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-105">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="5bcfd-106">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="5bcfd-107">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="5bcfd-108">In deze zelfstudie leert u hoe toodeliver op basis van locatie-pushmeldingen met Azure Notification Hubs en ruimtelijke Bing-gegevens, worden uit in de toepassing van een universele Windows-Platform.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-108">In this tutorial, you will learn how toodeliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5bcfd-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5bcfd-109">Prerequisites</span></span>
<span data-ttu-id="5bcfd-110">Allereerst omdat, moet u ervoor dat u alle Hallo software en service van de vereisten hebt toomake:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-110">First and foremost, you need toomake sure that you have all hello software and service pre-requisites:</span></span>

* <span data-ttu-id="5bcfd-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) of hoger ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) kan ook worden gebruikt).</span><span class="sxs-lookup"><span data-stu-id="5bcfd-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="5bcfd-112">Meest recente versie van Hallo [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5bcfd-112">Latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="5bcfd-113">[Bing Maps Dev Center-account](https://www.bingmapsportal.com/) (u kunt gratis een account maken en dit koppelen aan uw Microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="5bcfd-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="5bcfd-114">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="5bcfd-114">Getting Started</span></span>
<span data-ttu-id="5bcfd-115">Begint met het Hallo-project maken.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-115">Let’s start by creating hello project.</span></span> <span data-ttu-id="5bcfd-116">Open in Visual Studio een nieuw project van het type **Lege app (Universeel Windows)**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="5bcfd-117">Zodra Hallo project maken voltooid is, moet u Hallo basis voor Hallo app zelf te hebben.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-117">Once hello project creation is complete, you should have hello harness for hello app itself.</span></span> <span data-ttu-id="5bcfd-118">Nu gaan we alles instellen voor Hallo geofencing-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-118">Now let’s set up everything for hello geo-fencing infrastructure.</span></span> <span data-ttu-id="5bcfd-119">Omdat we continu toouse die Bing voor deze services zijn, is het een openbaar REST-API-eindpunt waarmee we tooquery specifieke locaties:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-119">Because we are going toouse Bing services for this, there is a public REST API endpoint that allows us tooquery specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="5bcfd-120">U moet toospecify Hallo volgende parameters tooget Hiermee aan de slag:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-120">You will need toospecify hello following parameters tooget it working:</span></span>

* <span data-ttu-id="5bcfd-121">De **gegevensbron-id** en de **gegevensbronnaam**. In de Bing Kaarten-API bevatten gegevensbronnen verschillende gerangschikte metagegevens, zoals locaties en bedrijfsuren.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="5bcfd-122">U kunt er hier meer over lezen.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-122">You can read more about those here.</span></span> 
* <span data-ttu-id="5bcfd-123">**Naam van de entiteit** – Hallo gewenste entiteit toouse als verwijzingspunt voor Hallo-melding.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-123">**Entity Name** – hello entity you want toouse as a reference point for hello notification.</span></span> 
* <span data-ttu-id="5bcfd-124">**Bing Maps API-sleutel** – dit is Hallo-sleutel die u eerder hebt verkregen tijdens het maken van Hallo Bing Dev Center-account.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-124">**Bing Maps API Key** – this is hello key that you obtained earlier when you created hello Bing Dev Center account.</span></span>

<span data-ttu-id="5bcfd-125">U gaat nu dieper op Hallo-instellingen voor elk van de bovenstaande Hallo-elementen.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-125">Let’s do a deep-dive on hello setup for each of hello elements above.</span></span>

## <a name="setting-up-hello-data-source"></a><span data-ttu-id="5bcfd-126">Hallo-gegevensbron instellen</span><span class="sxs-lookup"><span data-stu-id="5bcfd-126">Setting up hello data source</span></span>
<span data-ttu-id="5bcfd-127">U kunt dit doen in Hallo Bing Maps Dev Center.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-127">You can do it in hello Bing Maps Dev Center.</span></span> <span data-ttu-id="5bcfd-128">Klik op **gegevensbronnen** in Hallo in de bovenste navigatiebalk en selecteer **gegevensbronnen beheren**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-128">Simply click on **Data sources** in hello top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="5bcfd-129">Als u niet met Bing kaarten-API hebt gewerkt, waarschijnlijk er niet gegevensbronnen aanwezig is, zodat u kunt alleen een nieuwe classificatie door te klikken op het uploaden van de tooa-gegevensbron maken.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data tooa data source.</span></span> <span data-ttu-id="5bcfd-130">Zorg ervoor dat u alle vereiste Hallo velden invullen:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-130">Make sure you fill out all hello required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="5bcfd-131">U wellicht – wat Hallo gegevensbestand is en wat u moet uploaden?</span><span class="sxs-lookup"><span data-stu-id="5bcfd-131">You might be wondering – what is hello data file and what should you be uploading?</span></span> <span data-ttu-id="5bcfd-132">Voor Hallo doeleinden van deze test, kunnen we net Hallo-steekproef op basis van een pipe die een gebied van Hallo San Francisco kust frames gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-132">For hello purposes of this test, we can just use hello sample pipe-based that frames an area of hello San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="5bcfd-133">Hallo bovenstaande staat voor deze entiteit:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-133">hello above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="5bcfd-134">Gewoon Kopieer en plak Hallo bovenstaande tekenreeks in een nieuw bestand en sla het bestand als **NotificationHubsGeofence.pipe**, en upload het naar Hallo Bing Dev Center.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-134">Simply copy and paste hello string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in hello Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="5bcfd-135">Bent u mogelijk na vragen aan gebruiker toospecify een nieuwe sleutel voor Hallo **hoofdsleutel** die verschilt van Hallo **querysleutel**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-135">You might be prompted toospecify a new key for hello **Master Key** that is different from hello **Query Key**.</span></span> <span data-ttu-id="5bcfd-136">Gewoon een nieuwe sleutel via Hallo dashboard en vernieuw Hallo gegevens uploaden bronpagina maken.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-136">Simply create a new key through hello dashboard and refresh hello data source upload page.</span></span>
> 
> 

<span data-ttu-id="5bcfd-137">Zodra u Hallo gegevensbestand uploadt, moet u zeker dat u gegevensbron Hallo publiceren toomake.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-137">Once you upload hello data file, you will need toomake sure that you publish hello data source.</span></span> 

<span data-ttu-id="5bcfd-138">Ga te**gegevensbronnen beheren**, net zoals al eerder is gedaan, zoek de gegevensbron in Hallo lijst en klikt u op **publiceren** in Hallo **acties** kolom.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-138">Go too**Manage Data Sources**, just like we did above, find your data source in hello list and click on **Publish** in hello **Actions** column.</span></span> <span data-ttu-id="5bcfd-139">In een beetje ziet u de gegevensbron op Hallo **gepubliceerde gegevensbronnen** tabblad:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-139">In a bit, you should see your data source in hello **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="5bcfd-140">Als u op **bewerken**, u worden kunnen toosee in één oogopslag zien welke locaties er zijn geïntroduceerd in deze:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-140">If you click **Edit**, you will be able toosee at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="5bcfd-141">Hallo portal worden op dit moment geen Hallo van grenzen voor Hallo geofence die we hebben gemaakt – hoeft alleen een bevestiging dat Hallo locatie die is opgegeven is in de juiste nabijheid Hallo is weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-141">At this point, hello portal does not show you hello boundaries for hello geofence that we created – all we need is a confirmation that hello location specified is in hello right vicinity.</span></span>

<span data-ttu-id="5bcfd-142">U hebt nu alle Hallo-vereisten voor Hallo-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-142">Now you have all hello requirements for hello data source.</span></span> <span data-ttu-id="5bcfd-143">tooget hello op Hallo aanvraag-URL voor Hallo API-aanroep in Hallo Bing Maps Dev Center, klikt u op **gegevensbronnen** en selecteer **gegevensbroninformatie**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-143">tooget hello details on hello request URL for hello API call, in hello Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="5bcfd-144">Hallo **Query-URL** is wat zoekt.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-144">hello **Query URL** is what we’re after here.</span></span> <span data-ttu-id="5bcfd-145">Dit is Hallo-eindpunt op basis waarvan we toocheck query's uitvoeren kunt of Hallo-apparaat momenteel binnen de grenzen van een locatie Hallo of niet is.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-145">This is hello endpoint against which we can execute queries toocheck whether hello device is currently within hello boundaries of a location or not.</span></span> <span data-ttu-id="5bcfd-146">tooperform dit controleren, moet u een GET aanroepen tegen Hallo query-URL, met de volgende parameters toevoegt Hallo tooexecute:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-146">tooperform this check, we simply need tooexecute a GET call against hello query URL, with hello following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="5bcfd-147">Op die manier bent u een doelpunt dat we Hallo apparaat verkrijgen en Bing kaarten automatisch Hallo berekeningen toosee voert of binnen de geofence Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-147">That way you're specifying a target point that we obtain from hello device and Bing Maps will automatically perform hello calculations toosee whether it is within hello geofence.</span></span> <span data-ttu-id="5bcfd-148">Wanneer u Hallo-aanvraag via een browser (of cURL) uitvoert, ontvangt u standaard een JSON-antwoord:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-148">Once you execute hello request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="5bcfd-149">Dit antwoord gebeurt alleen als Hallo punt zich binnen de grenzen aangewezen Hallo.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-149">This response only happens when hello point is actually within hello designated boundaries.</span></span> <span data-ttu-id="5bcfd-150">Als dat niet het geval is, ontvangt u een lege **resultaten**bucket:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a><span data-ttu-id="5bcfd-151">Hallo UWP-toepassing instellen</span><span class="sxs-lookup"><span data-stu-id="5bcfd-151">Setting up hello UWP application</span></span>
<span data-ttu-id="5bcfd-152">Nu dat we Hallo gegevensbron gereed hebben, kunnen we gaan werken op Hallo UWP-toepassing die al eerder is geopend.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-152">Now that we have hello data source ready, we can start working on hello UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="5bcfd-153">U moet ten eerste de locatieservices inschakelen voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="5bcfd-154">toodo deze, dubbelklik op `Package.appxmanifest` bestanden per **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-154">toodo this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="5bcfd-155">Klik in het Hallo tabblad pakketeigenschappen dat zojuist is geopend, op **mogelijkheden** en zorg ervoor dat u selecteert **locatie**:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-155">In hello package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="5bcfd-156">Als het Hallo-locatiemogelijkheid is gedeclareerd, een nieuwe map maken in uw oplossing met de naam `Core`, en voeg een nieuw bestand naam `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-156">As hello location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="5bcfd-157">Hallo `LocationHelper` klasse zelf is op dit moment vrij algemeen: deze methode is kunnen we tooobtain Hallo gebruikerslocatie via Hallo systeem-API:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-157">hello `LocationHelper` class itself is fairly basic at this point – all it does is allow us tooobtain hello user location through hello system API:</span></span>

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

<span data-ttu-id="5bcfd-158">Lees meer over het ophalen van de locatie van gebruikers in uw UWP-apps Hallo officiële Hallo [MSDN-document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="5bcfd-158">You can read more about getting hello user’s location in UWP apps in hello official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="5bcfd-159">toocheck die Hallo locatie overname werkt, opent u Hallo codezijde van de hoofdpagina (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="5bcfd-159">toocheck that hello location acquisition is actually working, open hello code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="5bcfd-160">Maak een nieuwe gebeurtenis-handler voor Hallo `Loaded` gebeurtenis in Hallo `MainPage` constructor:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-160">Create a new event handler for hello `Loaded` event in hello `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="5bcfd-161">Hallo-implementatie van Hallo gebeurtenis-handler is als volgt:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-161">hello implementation of hello event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="5bcfd-162">Hallo-handler is gedeclareerd als asynchroon omdat `GetCurrentLocation` afwachtend is en daarom vereist toobe uitgevoerd in een asynchrone context.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-162">Notice that we declared hello handler as async because `GetCurrentLocation` is awaitable, and therefore requires toobe executed in an async context.</span></span> <span data-ttu-id="5bcfd-163">Bovendien omdat onder bepaalde omstandigheden we met een null-locatie eindigen mogelijk (bijvoorbeeld Hallo locatie-services zijn uitgeschakeld of machtigingen tooaccess locatie is geweigerd door de toepassing hello), moeten we toomake ervoor dat dit goed wordt afgehandeld met een null-controle.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-163">Also, because under certain circumstances we might end up with a null location (e.g. hello location services are disabled or hello application was denied permissions tooaccess location), we need toomake sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="5bcfd-164">Hallo-toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-164">Run hello application.</span></span> <span data-ttu-id="5bcfd-165">Controleer of u toegang tot de locatie toestaat:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="5bcfd-166">Eenmaal Hallo toepassing is gestart, moet u kunnen toosee Hallo coördinaten in Hallo **uitvoer** venster:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-166">Once hello application launches, you should be able toosee hello coordinates in hello **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="5bcfd-167">Nu weet u locatie overname werkt – denken gratis tooremove Hallo test gebeurtenis-handler voor geladen, omdat we niet gebruikt het niet meer.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-167">Now you know that location acquisition works – feel free tooremove hello test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="5bcfd-168">de volgende stap Hallo is toocapture locatiewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-168">hello next step is toocapture location changes.</span></span> <span data-ttu-id="5bcfd-169">Daarvoor daarvoor gaat u terug toohello `LocationHelper` klasse en het toevoegen van Hallo gebeurtenis-handler voor `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-169">For that, let’s go back toohello `LocationHelper` class and add hello event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="5bcfd-170">Hallo implementatie Hallo locatiecoördinaten weergegeven in Hallo **uitvoer** venster:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-170">hello implementation will show hello location coordinates in hello **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a><span data-ttu-id="5bcfd-171">Hallo back-end instellen</span><span class="sxs-lookup"><span data-stu-id="5bcfd-171">Setting up hello backend</span></span>
<span data-ttu-id="5bcfd-172">Hallo downloaden [.NET-back-Endvoorbeeld via GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="5bcfd-172">Download hello [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="5bcfd-173">Zodra het Hallo downloaden is voltooid, opent u Hallo `NotifyUsers` map en vervolgens Hallo `NotifyUsers.sln` bestand.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-173">Once hello download completes, open hello `NotifyUsers` folder, and subsequently – hello `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="5bcfd-174">Set Hallo `AppBackend` project als Hallo **opstartproject** en deze te starten.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-174">Set hello `AppBackend` project as hello **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="5bcfd-175">Hallo project is al geconfigureerd toosend push notifications tootarget apparaten, dus moeten we er slechts twee dingen toodo – wisselen van de juiste verbindingsreeks Hallo voor Hallo notification hub en grens identificatie toosend Hallo melding alleen wanneer hello toevoegen gebruiker is binnen Hallo geofence bevindt.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-175">hello project is already configured toosend push notifications tootarget devices, so we’ll need toodo only two things – swap out hello right connection string for hello notification hub and add boundary identification toosend hello notification only when hello user is within hello geofence.</span></span>

<span data-ttu-id="5bcfd-176">tooconfigure hello verbindingsreeks, in Hallo `Models` map open `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-176">tooconfigure hello connection string, in hello `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="5bcfd-177">Hallo `NotificationHubClient.CreateClientFromConnectionString` functie mogen bevatten informatie over de notification hub die u in Hallo krijgen kunt Hallo [Azure Portal](https://portal.azure.com) (Hallo inzien **toegangsbeleid** blade in  **Instellingen**).</span><span class="sxs-lookup"><span data-stu-id="5bcfd-177">hello `NotificationHubClient.CreateClientFromConnectionString` function should contain hello information about your notification hub that you can get in hello [Azure Portal](https://portal.azure.com) (look inside hello **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="5bcfd-178">Sla het bijgewerkte configuratiebestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-178">Save hello updated configuration file.</span></span>

<span data-ttu-id="5bcfd-179">Er moet nu toocreate een model voor Hallo Bing kaarten-API-resultaat.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-179">Now we need toocreate a model for hello Bing Maps API result.</span></span> <span data-ttu-id="5bcfd-180">Hallo gemakkelijkste manier toodo die met de rechtermuisknop op Hallo `Models` map **toevoegen** > **klasse**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-180">hello easiest way toodo that is right-click on hello `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="5bcfd-181">Noem deze `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="5bcfd-182">Hierna Hallo JSON uit Hallo API-reactie die is besproken in de eerste sectie hello en in Visual Studio gebruik kopiëren **bewerken** > **Plakken speciaal** > **Paste JSON Als klassen**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-182">Once done, copy hello JSON from hello API response that we discussed in hello first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="5bcfd-183">Op deze manier zorgt u ervoor dat object Hallo zullen worden gedeserialiseerd precies zoals bedoeld was.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-183">That way we ensure that hello object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="5bcfd-184">De resulterende klasseset ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-184">Your resulting class set should resemble this:</span></span>

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

<span data-ttu-id="5bcfd-185">Open vervolgens `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="5bcfd-186">Moeten we tooaccount tootweak Hallo Post-aanroep voor Hallo doel breedtegraad.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-186">We need tootweak hello Post call tooaccount for hello target longitude and latitude.</span></span> <span data-ttu-id="5bcfd-187">Daarvoor toe te voegen twee tekenreeksen toohello-functiehandtekening: `latitude` en `longitude`.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-187">For that, simply add two strings toohello function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="5bcfd-188">Maak een nieuwe klasse binnen Hallo project met de naam `ApiHelper.cs` : we gebruiken deze tooconnect tooBing toocheck punt grens snijpunten.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-188">Create a new class within hello project called `ApiHelper.cs` – we’ll use it tooconnect tooBing toocheck point boundary intersections.</span></span> <span data-ttu-id="5bcfd-189">Implementeer als volgt een `IsPointWithinBounds`-functie:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="5bcfd-190">Zorg ervoor dat toosubstitute Hallo API-eindpunt met Hallo query-URL die u eerder hebt verkregen via Hallo Bing Dev Center (dit geldt ook toohello API-sleutel).</span><span class="sxs-lookup"><span data-stu-id="5bcfd-190">Make sure toosubstitute hello API endpoint with hello query URL that you obtained earlier from hello Bing Dev Center (same applies toohello API key).</span></span> 
> 
> 

<span data-ttu-id="5bcfd-191">Als er resultaten toohello query, dat betekent dat het opgegeven punt Hallo is binnen de grenzen Hallo van Hallo geofence wordt dan geretourneerd `true`.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-191">If there are results toohello query, that means that hello specified point is within hello boundaries of hello geofence, so we return `true`.</span></span> <span data-ttu-id="5bcfd-192">Als er geen resultaten zijn, Bing is laat weten we dat Hallo punt buiten Hallo kader bevindt, wordt dan geretourneerd `false`.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-192">If there are no results, Bing is telling us that hello point is outside hello lookup frame, so we return `false`.</span></span>

<span data-ttu-id="5bcfd-193">Terug in de `NotificationsController.cs`, een controle aan vóór Hallo switch-instructie maken:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-193">Back in `NotificationsController.cs`, create a check right before hello switch statement:</span></span>

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

<span data-ttu-id="5bcfd-194">Op die manier Hallo er alleen meldingen verzonden wanneer Hallo punt zich binnen Hallo grenzen.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-194">That way, hello notification is only sent when hello point is within hello boundaries.</span></span>

## <a name="testing-push-notifications-in-hello-uwp-app"></a><span data-ttu-id="5bcfd-195">Pushmeldingen testen in Hallo UWP-app</span><span class="sxs-lookup"><span data-stu-id="5bcfd-195">Testing push notifications in hello UWP app</span></span>
<span data-ttu-id="5bcfd-196">Als u terugkeert toohello UWP-app, er worden nu kunnen tootest meldingen.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-196">Going back toohello UWP app, we should now be able tootest notifications.</span></span> <span data-ttu-id="5bcfd-197">Binnen Hallo `LocationHelper` klasse, maakt u een nieuwe functie – `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-197">Within hello `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="5bcfd-198">Hallo wisselen `POST_URL` toohello locatie van de geïmplementeerde webtoepassing die in de vorige sectie Hallo is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-198">Swap hello `POST_URL` toohello location of your deployed web application that we created in hello previous section.</span></span> <span data-ttu-id="5bcfd-199">Op dit moment is OK toorun het lokaal, maar als u werkt over het implementeren van een openbare versie, moet u toohost deze met een externe provider.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-199">For now, it’s OK toorun it locally, but as you work on deploying a public version, you will need toohost it with an external provider.</span></span>
> 
> 

<span data-ttu-id="5bcfd-200">Zorg ervoor dat we Hallo UWP-app voor pushmeldingen registreren.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-200">Let’s now make sure that we register hello UWP app for push notifications.</span></span> <span data-ttu-id="5bcfd-201">Klik in Visual Studio op **Project** > **opslaan** > **app koppelen aan Hallo store**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-201">In Visual Studio, click on **Project** > **Store** > **Associate app with hello store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="5bcfd-202">Zodra u zich aanmeldt tooyour developer-account, moet u een bestaande app selecteren of een nieuwe maken en Hallo pakket koppelen.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-202">Once you sign in tooyour developer account, make sure you select an existing app or create a new one and associate hello package with it.</span></span> 

<span data-ttu-id="5bcfd-203">Ga toohello Dev Center en open Hallo-app die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-203">Go toohello Dev Center and open hello app that you just created.</span></span> <span data-ttu-id="5bcfd-204">Klik op **Services** > **Pushmeldingen** > **Live Services site**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="5bcfd-205">Op Hallo-site, dient u Hallo **Toepassingsgeheim** en Hallo **pakket-SID**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-205">On hello site, take note of hello **Application Secret** and hello **Package SID**.</span></span> <span data-ttu-id="5bcfd-206">U moet zowel in hello Azure Portal – open de notification hub, klikt u op **instellingen** > **Notification Services** > **Windows (WNS)**en Voer Hallo-gegevens in velden Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-206">You will need both in hello Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter hello information in hello required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="5bcfd-207">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-207">Click on **Save**.</span></span>

<span data-ttu-id="5bcfd-208">Klik met de rechtermuisknop op **Verwijzingen** in **Solution Explorer** en kies **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="5bcfd-209">Moet een verwijzing toohello tooadd **Microsoft Azure Service Bus beheerde bibliotheek** – zoek naar `WindowsAzure.Messaging.Managed` en toe te voegen tooyour project.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-209">We will need tooadd a reference toohello **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it tooyour project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="5bcfd-210">Voor testdoeleinden, maken we Hallo `MainPage_Loaded` nogmaals: gebeurtenis-handler en voeg deze code codefragment tooit:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-210">For testing purposes, we can create hello `MainPage_Loaded` event handler once again, and add this code snippet tooit:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="5bcfd-211">Hallo hierboven wordt Hallo-app voor Hallo notification hub geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-211">hello above registers hello app with hello notification hub.</span></span> <span data-ttu-id="5bcfd-212">U bent klaar toogo.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-212">You are ready toogo!</span></span> 

<span data-ttu-id="5bcfd-213">In `LocationHelper`, binnen Hallo `Geolocator_PositionChanged` handler, kunt u een testcodefragment die geforceerd Hallo locatie binnen de geofence Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-213">In `LocationHelper`, inside hello `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put hello location inside hello geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="5bcfd-214">Omdat we Hallo echte coördinaten (die misschien niet binnen de grenzen van Hallo Hallo momenteel) niet doorgeeft en vooraf gedefinieerde testwaarden gebruikt, zien we een melding weergegeven op de update:</span><span class="sxs-lookup"><span data-stu-id="5bcfd-214">Because we are not passing hello real coordinates (which might not be within hello boundaries at hello moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="5bcfd-215">Wat nu?</span><span class="sxs-lookup"><span data-stu-id="5bcfd-215">What’s next?</span></span>
<span data-ttu-id="5bcfd-216">Er zijn een aantal stappen dat u wellicht toofollow in toevoeging toohello hierboven toomake ervoor dat de oplossing Hallo gereed is voor productie.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-216">There are a couple of steps that you might need toofollow in addition toohello above toomake sure that hello solution is production-ready.</span></span>

<span data-ttu-id="5bcfd-217">Allereerst omdat, moet u mogelijk tooensure dat de geofences dynamisch zijn.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-217">First and foremost, you might need tooensure that geofences are dynamic.</span></span> <span data-ttu-id="5bcfd-218">Hiervoor moet een aantal extra werk met hello Bing-API in volgorde toobe kunnen tooupload nieuwe grenzen binnen Hallo bestaande gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-218">This will require some extra work with hello Bing API in order toobe able tooupload new boundaries within hello existing data source.</span></span> <span data-ttu-id="5bcfd-219">Raadpleeg Hallo [Bing Spatial Data Services-API-documentatie](https://msdn.microsoft.com/library/ff701734.aspx) voor meer informatie over Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-219">Consult hello [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on hello subject.</span></span>

<span data-ttu-id="5bcfd-220">Ten tweede, aangezien u werkende tooensure dat Hallo levering toohello juiste deelnemers wordt gedaan, kunt u tootarget ze via [tagging](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="5bcfd-220">Second, as you are working tooensure that hello delivery is done toohello right participants, you might want tootarget them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="5bcfd-221">de bovenstaande Hallo-oplossing beschrijft een scenario waarin u een groot aantal verschillende doelplatforms, wellicht zodat we toosystem specifieke functies van Hallo geofencing niet beperkt.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-221">hello solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit hello geofencing toosystem-specific capabilities.</span></span> <span data-ttu-id="5bcfd-222">Die gezegd, Hallo universele Windows-Platform biedt mogelijkheden te[detecteren van geofences rechts out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="5bcfd-222">That said, hello Universal Windows Platform offers capabilities too[detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="5bcfd-223">Zie onze [documentatieportal](https://azure.microsoft.com/documentation/services/notification-hubs/) voor meer informatie over Notification Hubs-mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="5bcfd-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>


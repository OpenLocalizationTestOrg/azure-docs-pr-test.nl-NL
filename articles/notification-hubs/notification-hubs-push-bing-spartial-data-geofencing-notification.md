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
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a>Pushmeldingen met geofencing verzenden met Azure Notification Hubs en ruimtelijke Bing-gegevens
> [!NOTE]
> toocomplete deze zelfstudie maakt u een actief Azure-account moet hebben. Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02) voor meer informatie.
> 
> 

In deze zelfstudie leert u hoe toodeliver op basis van locatie-pushmeldingen met Azure Notification Hubs en ruimtelijke Bing-gegevens, worden uit in de toepassing van een universele Windows-Platform.

## <a name="prerequisites"></a>Vereisten
Allereerst omdat, moet u ervoor dat u alle Hallo software en service van de vereisten hebt toomake:

* [Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) of hoger ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) kan ook worden gebruikt). 
* Meest recente versie van Hallo [Azure SDK](https://azure.microsoft.com/downloads/). 
* [Bing Maps Dev Center-account](https://www.bingmapsportal.com/) (u kunt gratis een account maken en dit koppelen aan uw Microsoft-account). 

## <a name="getting-started"></a>Aan de slag
Begint met het Hallo-project maken. Open in Visual Studio een nieuw project van het type **Lege app (Universeel Windows)**.

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

Zodra Hallo project maken voltooid is, moet u Hallo basis voor Hallo app zelf te hebben. Nu gaan we alles instellen voor Hallo geofencing-infrastructuur. Omdat we continu toouse die Bing voor deze services zijn, is het een openbaar REST-API-eindpunt waarmee we tooquery specifieke locaties:

    http://spatial.virtualearth.net/REST/v1/data/

U moet toospecify Hallo volgende parameters tooget Hiermee aan de slag:

* De **gegevensbron-id** en de **gegevensbronnaam**. In de Bing Kaarten-API bevatten gegevensbronnen verschillende gerangschikte metagegevens, zoals locaties en bedrijfsuren. U kunt er hier meer over lezen. 
* **Naam van de entiteit** – Hallo gewenste entiteit toouse als verwijzingspunt voor Hallo-melding. 
* **Bing Maps API-sleutel** – dit is Hallo-sleutel die u eerder hebt verkregen tijdens het maken van Hallo Bing Dev Center-account.

U gaat nu dieper op Hallo-instellingen voor elk van de bovenstaande Hallo-elementen.

## <a name="setting-up-hello-data-source"></a>Hallo-gegevensbron instellen
U kunt dit doen in Hallo Bing Maps Dev Center. Klik op **gegevensbronnen** in Hallo in de bovenste navigatiebalk en selecteer **gegevensbronnen beheren**.

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

Als u niet met Bing kaarten-API hebt gewerkt, waarschijnlijk er niet gegevensbronnen aanwezig is, zodat u kunt alleen een nieuwe classificatie door te klikken op het uploaden van de tooa-gegevensbron maken. Zorg ervoor dat u alle vereiste Hallo velden invullen:

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

U wellicht – wat Hallo gegevensbestand is en wat u moet uploaden? Voor Hallo doeleinden van deze test, kunnen we net Hallo-steekproef op basis van een pipe die een gebied van Hallo San Francisco kust frames gebruiken:

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

Hallo bovenstaande staat voor deze entiteit:

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

Gewoon Kopieer en plak Hallo bovenstaande tekenreeks in een nieuw bestand en sla het bestand als **NotificationHubsGeofence.pipe**, en upload het naar Hallo Bing Dev Center.

> [!NOTE]
> Bent u mogelijk na vragen aan gebruiker toospecify een nieuwe sleutel voor Hallo **hoofdsleutel** die verschilt van Hallo **querysleutel**. Gewoon een nieuwe sleutel via Hallo dashboard en vernieuw Hallo gegevens uploaden bronpagina maken.
> 
> 

Zodra u Hallo gegevensbestand uploadt, moet u zeker dat u gegevensbron Hallo publiceren toomake. 

Ga te**gegevensbronnen beheren**, net zoals al eerder is gedaan, zoek de gegevensbron in Hallo lijst en klikt u op **publiceren** in Hallo **acties** kolom. In een beetje ziet u de gegevensbron op Hallo **gepubliceerde gegevensbronnen** tabblad:

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

Als u op **bewerken**, u worden kunnen toosee in één oogopslag zien welke locaties er zijn geïntroduceerd in deze:

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

Hallo portal worden op dit moment geen Hallo van grenzen voor Hallo geofence die we hebben gemaakt – hoeft alleen een bevestiging dat Hallo locatie die is opgegeven is in de juiste nabijheid Hallo is weergegeven.

U hebt nu alle Hallo-vereisten voor Hallo-gegevensbron. tooget hello op Hallo aanvraag-URL voor Hallo API-aanroep in Hallo Bing Maps Dev Center, klikt u op **gegevensbronnen** en selecteer **gegevensbroninformatie**.

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

Hallo **Query-URL** is wat zoekt. Dit is Hallo-eindpunt op basis waarvan we toocheck query's uitvoeren kunt of Hallo-apparaat momenteel binnen de grenzen van een locatie Hallo of niet is. tooperform dit controleren, moet u een GET aanroepen tegen Hallo query-URL, met de volgende parameters toevoegt Hallo tooexecute:

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

Op die manier bent u een doelpunt dat we Hallo apparaat verkrijgen en Bing kaarten automatisch Hallo berekeningen toosee voert of binnen de geofence Hallo opgeven. Wanneer u Hallo-aanvraag via een browser (of cURL) uitvoert, ontvangt u standaard een JSON-antwoord:

![](./media/notification-hubs-geofence/bing-maps-json.png)

Dit antwoord gebeurt alleen als Hallo punt zich binnen de grenzen aangewezen Hallo. Als dat niet het geval is, ontvangt u een lege **resultaten**bucket:

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a>Hallo UWP-toepassing instellen
Nu dat we Hallo gegevensbron gereed hebben, kunnen we gaan werken op Hallo UWP-toepassing die al eerder is geopend.

U moet ten eerste de locatieservices inschakelen voor de toepassing. toodo deze, dubbelklik op `Package.appxmanifest` bestanden per **Solution Explorer**.

![](./media/notification-hubs-geofence/vs-package-manifest.png)

Klik in het Hallo tabblad pakketeigenschappen dat zojuist is geopend, op **mogelijkheden** en zorg ervoor dat u selecteert **locatie**:

![](./media/notification-hubs-geofence/vs-package-location.png)

Als het Hallo-locatiemogelijkheid is gedeclareerd, een nieuwe map maken in uw oplossing met de naam `Core`, en voeg een nieuw bestand naam `LocationHelper.cs`:

![](./media/notification-hubs-geofence/vs-location-helper.png)

Hallo `LocationHelper` klasse zelf is op dit moment vrij algemeen: deze methode is kunnen we tooobtain Hallo gebruikerslocatie via Hallo systeem-API:

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

Lees meer over het ophalen van de locatie van gebruikers in uw UWP-apps Hallo officiële Hallo [MSDN-document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).

toocheck die Hallo locatie overname werkt, opent u Hallo codezijde van de hoofdpagina (`MainPage.xaml.cs`). Maak een nieuwe gebeurtenis-handler voor Hallo `Loaded` gebeurtenis in Hallo `MainPage` constructor:

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

Hallo-implementatie van Hallo gebeurtenis-handler is als volgt:

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

Hallo-handler is gedeclareerd als asynchroon omdat `GetCurrentLocation` afwachtend is en daarom vereist toobe uitgevoerd in een asynchrone context. Bovendien omdat onder bepaalde omstandigheden we met een null-locatie eindigen mogelijk (bijvoorbeeld Hallo locatie-services zijn uitgeschakeld of machtigingen tooaccess locatie is geweigerd door de toepassing hello), moeten we toomake ervoor dat dit goed wordt afgehandeld met een null-controle.

Hallo-toepassing uitvoeren. Controleer of u toegang tot de locatie toestaat:

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

Eenmaal Hallo toepassing is gestart, moet u kunnen toosee Hallo coördinaten in Hallo **uitvoer** venster:

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

Nu weet u locatie overname werkt – denken gratis tooremove Hallo test gebeurtenis-handler voor geladen, omdat we niet gebruikt het niet meer.

de volgende stap Hallo is toocapture locatiewijzigingen. Daarvoor daarvoor gaat u terug toohello `LocationHelper` klasse en het toevoegen van Hallo gebeurtenis-handler voor `PositionChanged`:

    geolocator.PositionChanged += Geolocator_PositionChanged;

Hallo implementatie Hallo locatiecoördinaten weergegeven in Hallo **uitvoer** venster:

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a>Hallo back-end instellen
Hallo downloaden [.NET-back-Endvoorbeeld via GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). Zodra het Hallo downloaden is voltooid, opent u Hallo `NotifyUsers` map en vervolgens Hallo `NotifyUsers.sln` bestand.

Set Hallo `AppBackend` project als Hallo **opstartproject** en deze te starten.

![](./media/notification-hubs-geofence/vs-startup-project.png)

Hallo project is al geconfigureerd toosend push notifications tootarget apparaten, dus moeten we er slechts twee dingen toodo – wisselen van de juiste verbindingsreeks Hallo voor Hallo notification hub en grens identificatie toosend Hallo melding alleen wanneer hello toevoegen gebruiker is binnen Hallo geofence bevindt.

tooconfigure hello verbindingsreeks, in Hallo `Models` map open `Notifications.cs`. Hallo `NotificationHubClient.CreateClientFromConnectionString` functie mogen bevatten informatie over de notification hub die u in Hallo krijgen kunt Hallo [Azure Portal](https://portal.azure.com) (Hallo inzien **toegangsbeleid** blade in  **Instellingen**). Sla het bijgewerkte configuratiebestand Hallo.

Er moet nu toocreate een model voor Hallo Bing kaarten-API-resultaat. Hallo gemakkelijkste manier toodo die met de rechtermuisknop op Hallo `Models` map **toevoegen** > **klasse**. Noem deze `GeofenceBoundary.cs`. Hierna Hallo JSON uit Hallo API-reactie die is besproken in de eerste sectie hello en in Visual Studio gebruik kopiëren **bewerken** > **Plakken speciaal** > **Paste JSON Als klassen**. 

Op deze manier zorgt u ervoor dat object Hallo zullen worden gedeserialiseerd precies zoals bedoeld was. De resulterende klasseset ziet er als volgt uit:

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

Open vervolgens `Controllers` > `NotificationsController.cs`. Moeten we tooaccount tootweak Hallo Post-aanroep voor Hallo doel breedtegraad. Daarvoor toe te voegen twee tekenreeksen toohello-functiehandtekening: `latitude` en `longitude`.

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

Maak een nieuwe klasse binnen Hallo project met de naam `ApiHelper.cs` : we gebruiken deze tooconnect tooBing toocheck punt grens snijpunten. Implementeer als volgt een `IsPointWithinBounds`-functie:

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
> Zorg ervoor dat toosubstitute Hallo API-eindpunt met Hallo query-URL die u eerder hebt verkregen via Hallo Bing Dev Center (dit geldt ook toohello API-sleutel). 
> 
> 

Als er resultaten toohello query, dat betekent dat het opgegeven punt Hallo is binnen de grenzen Hallo van Hallo geofence wordt dan geretourneerd `true`. Als er geen resultaten zijn, Bing is laat weten we dat Hallo punt buiten Hallo kader bevindt, wordt dan geretourneerd `false`.

Terug in de `NotificationsController.cs`, een controle aan vóór Hallo switch-instructie maken:

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

Op die manier Hallo er alleen meldingen verzonden wanneer Hallo punt zich binnen Hallo grenzen.

## <a name="testing-push-notifications-in-hello-uwp-app"></a>Pushmeldingen testen in Hallo UWP-app
Als u terugkeert toohello UWP-app, er worden nu kunnen tootest meldingen. Binnen Hallo `LocationHelper` klasse, maakt u een nieuwe functie – `SendLocationToBackend`:

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
> Hallo wisselen `POST_URL` toohello locatie van de geïmplementeerde webtoepassing die in de vorige sectie Hallo is gemaakt. Op dit moment is OK toorun het lokaal, maar als u werkt over het implementeren van een openbare versie, moet u toohost deze met een externe provider.
> 
> 

Zorg ervoor dat we Hallo UWP-app voor pushmeldingen registreren. Klik in Visual Studio op **Project** > **opslaan** > **app koppelen aan Hallo store**.

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

Zodra u zich aanmeldt tooyour developer-account, moet u een bestaande app selecteren of een nieuwe maken en Hallo pakket koppelen. 

Ga toohello Dev Center en open Hallo-app die u zojuist hebt gemaakt. Klik op **Services** > **Pushmeldingen** > **Live Services site**.

![](./media/notification-hubs-geofence/ms-live-services.png)

Op Hallo-site, dient u Hallo **Toepassingsgeheim** en Hallo **pakket-SID**. U moet zowel in hello Azure Portal – open de notification hub, klikt u op **instellingen** > **Notification Services** > **Windows (WNS)**en Voer Hallo-gegevens in velden Hallo vereist.

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

Klik op **Opslaan**.

Klik met de rechtermuisknop op **Verwijzingen** in **Solution Explorer** en kies **NuGet-pakketten beheren**. Moet een verwijzing toohello tooadd **Microsoft Azure Service Bus beheerde bibliotheek** – zoek naar `WindowsAzure.Messaging.Managed` en toe te voegen tooyour project.

![](./media/notification-hubs-geofence/vs-nuget.png)

Voor testdoeleinden, maken we Hallo `MainPage_Loaded` nogmaals: gebeurtenis-handler en voeg deze code codefragment tooit:

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

Hallo hierboven wordt Hallo-app voor Hallo notification hub geregistreerd. U bent klaar toogo. 

In `LocationHelper`, binnen Hallo `Geolocator_PositionChanged` handler, kunt u een testcodefragment die geforceerd Hallo locatie binnen de geofence Hallo toevoegen:

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

Omdat we Hallo echte coördinaten (die misschien niet binnen de grenzen van Hallo Hallo momenteel) niet doorgeeft en vooraf gedefinieerde testwaarden gebruikt, zien we een melding weergegeven op de update:

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a>Wat nu?
Er zijn een aantal stappen dat u wellicht toofollow in toevoeging toohello hierboven toomake ervoor dat de oplossing Hallo gereed is voor productie.

Allereerst omdat, moet u mogelijk tooensure dat de geofences dynamisch zijn. Hiervoor moet een aantal extra werk met hello Bing-API in volgorde toobe kunnen tooupload nieuwe grenzen binnen Hallo bestaande gegevensbron. Raadpleeg Hallo [Bing Spatial Data Services-API-documentatie](https://msdn.microsoft.com/library/ff701734.aspx) voor meer informatie over Hallo onderwerp.

Ten tweede, aangezien u werkende tooensure dat Hallo levering toohello juiste deelnemers wordt gedaan, kunt u tootarget ze via [tagging](notification-hubs-tags-segment-push-message.md).

de bovenstaande Hallo-oplossing beschrijft een scenario waarin u een groot aantal verschillende doelplatforms, wellicht zodat we toosystem specifieke functies van Hallo geofencing niet beperkt. Die gezegd, Hallo universele Windows-Platform biedt mogelijkheden te[detecteren van geofences rechts out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).

Zie onze [documentatieportal](https://azure.microsoft.com/documentation/services/notification-hubs/) voor meer informatie over Notification Hubs-mogelijkheden.


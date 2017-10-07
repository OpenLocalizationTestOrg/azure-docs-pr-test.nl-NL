---
title: aaaRegistration Management
description: Dit onderwerp wordt uitgelegd hoe apparaten met notification hubs in volgorde tooreceive tooregister pushmeldingen.
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: fd0ee230-132c-4143-b4f9-65cef7f463a1
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 76471a45c7a0da1614ceed82b73cdb3319979ff7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="registration-management"></a>Registratiebeheer
## <a name="overview"></a>Overzicht
Dit onderwerp wordt uitgelegd hoe apparaten met notification hubs in volgorde tooreceive tooregister pushmeldingen. Hallo onderwerp beschrijft registraties op hoog niveau en vervolgens maakt u kennis met Hallo twee belangrijkste patronen voor het registreren van apparaten: registreren van Hallo apparaat rechtstreeks toohello notification hub en registreren via een back-end voor de toepassing. 

## <a name="what-is-device-registration"></a>Wat is de registratie
Registreren van apparaten met een Notification Hub wordt bereikt met een **registratie** of **installatie**.

#### <a name="registrations"></a>Registraties
Een registratie koppelt Hallo Platform Notification Service (PNS) voor een apparaat met tags en mogelijk een sjabloon verwerkt. Hallo PNS-ingang is mogelijk een ChannelURI, apparaattoken of GCM-registratie-id. Labels zijn gebruikte tooroute meldingen toohello correcte set apparaat verwerkt. Zie voor meer informatie [Routering en code-expressies](notification-hubs-tags-segment-push-message.md). Sjablonen zijn gebruikte tooimplement per registratie transformatie. Zie voor meer informatie [sjablonen](notification-hubs-templates-cross-platform-push-messages.md).

#### <a name="installations"></a>Installaties
Een installatie is een uitgebreide registratie met een groot aantal push gerelateerd eigenschappen. Is het nieuwste en beste aanpak tooregistering Hallo uw apparaten. Echter niet ondersteund door de clientkant .NET SDK ([Notification Hub SDK voor back-end-bewerkingen](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) vanaf nog.  Dit betekent dat als u van clientapparaat Hallo zichzelf registreert, hebt u toouse hello [Notification Hubs REST-API](https://msdn.microsoft.com/library/mt621153.aspx) toosupport installaties benaderen. Als u een back-endservice gebruikt, moet u kunnen toouse [Notification Hub SDK voor back-end-bewerkingen](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Hallo Hieronder volgen enkele belangrijke voordelen toousing installaties:

* Maken of bijwerken van een installatie is volledig idempotent. Zo kunt u het opnieuw zonder vragen over dubbele registraties.
* Hallo installatiemodel maakt het eenvoudig toodo afzonderlijke pushes - doelen specifiek apparaat. Een Systeemlabel **' $InstallationId: [omwille van] '** automatisch met elke installatie op basis van de registratie wordt toegevoegd. Zo kunt u bellen een verzenden toothis tag tootarget een specifiek apparaat zonder toodo extra programmeren.
* Installaties ook kunt u toodo gedeeltelijke registratie-updates. Hallo gedeeltelijke update van een installatie wordt aangevraagd met een PATCH-methode met Hallo [JSON-Patch standaard](https://tools.ietf.org/html/rfc6902). Dit is vooral handig als u wilt dat tooupdate labels op Hallo registratie. U heb toopull omlaag Hallo volledige registratie en alle eerdere Hallo-codes opnieuw opnieuw te verzenden.

Een installatie kan Hallo Hallo volgende eigenschappen bevatten. Voor een volledig overzicht van Hallo installatie-eigenschappen Zie [maken of een installatie met REST-API worden overschreven](https://msdn.microsoft.com/library/azure/mt621153.aspx) of [installatie-eigenschappen](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) voor Hallo.

    // Example installation format tooshow some supported properties
    {
        installationId: "",
        expirationTime: "",
        tags: [],
        platform: "",
        pushChannel: "",
        ………
        templates: {
            "templateName1" : {
                body: "",
                tags: [] },
            "templateName2" : {
                body: "",
                // Headers are for Windows Store only
                headers: {
                    "X-WNS-Type": "wns/tile" }
                tags: [] }
        },
        secondaryTiles: {
            "tileId1": {
                pushChannel: "",
                tags: [],
                templates: {
                    "otherTemplate": {
                        bodyTemplate: "",
                        headers: {
                            ... }
                        tags: [] }
                }
            }
        }
    }



Het is belangrijk toonote waarop registraties en installaties standaard niet meer geldig.

Registraties en installaties moeten een geldige PNS-ingang voor elk apparaat/kanaal bevatten. Omdat PNS-ingangen kunnen alleen worden verkregen in een client-app op Hallo-apparaat, is een patroon tooregister rechtstreeks op het apparaat met Hallo client-app. Op Hallo gerelateerde andere hand, beveiligingsoverwegingen en bedrijfslogica tootags moet u mogelijk toomanage apparaatregistratie in de back-end van Hallo-app. 

#### <a name="templates"></a>Sjablonen
Als u wilt dat toouse [sjablonen](notification-hubs-templates-cross-platform-push-messages.md), de installatie van apparaat Hallo houdt ook alle sjablonen die zijn gekoppeld aan het apparaat in een JSON formatteren (Zie het bovenstaande voorbeeld). Hallo sjabloonnamen helpen verschillende sjablonen voor Hallo gericht hetzelfde apparaat.

Houd er rekening mee dat de sjabloonnaam van elke tooa sjabloon instantie en een optionele set van labels toegewezen. Elk platform kunt bovendien aanvullende Sjablooneigenschappen hebben. Voor Windows Store (met WNS) en Windows Phone 8 (met behulp van MPNS), kan een extra set van headers deel uitmaken van Hallo-sjabloon. In geval van APNs Hallo kunt u een eigenschap verstrijken tooeither een sjabloonexpressie-constante of -tooa instellen. Voor een volledig overzicht van Hallo installatie-eigenschappen Zie [maken of een installatie met REST overschrijven](https://msdn.microsoft.com/library/azure/mt621153.aspx) onderwerp.

#### <a name="secondary-tiles-for-windows-store-apps"></a>Secundaire tegels voor Windows Store-Apps
Voor Windows Store-clienttoepassingen Hallo verzenden van meldingen toosecondary tegels is hetzelfde als het verzenden van toohello primaire alias. Dit wordt ook ondersteund in installaties. Houd er rekening mee dat secundaire tegels een verschillende ChannelUri hebben, welke Hallo SDK op uw clientapp transparant verwerkt.

Hallo SecondaryTiles woordenlijst gebruikt Hallo dezelfde TileId die gebruikte toocreate hello SecondaryTiles object in de Windows Store-app.
Als de primaire ChannelUri, ChannelUris secundaire tegels Hello op elk moment wijzigen kunt. In de volgorde tookeep Hallo installaties in Hallo notification hub is bijgewerkt Hallo apparaat ze hebt vernieuwd Hello huidige ChannelUris Hallo secundaire tegels.

## <a name="registration-management-from-hello-device"></a>Beheer van de registratie van Hallo-apparaat
Bij het beheren van de registratie van de client-apps, is alleen Hallo back-end die verantwoordelijk is voor het verzenden van meldingen. Client-apps PNS-ingangen up toodate houden en registreer labels. Hallo volgende afbeelding ziet u dit patroon.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

Hallo apparaat eerst Hallo PNS verwerken opgehaald uit Hallo PNS vervolgens rechtstreeks voor Hallo notification hub geregistreerd. Nadat het Hallo-registratie is geslaagd, kan back-end Hallo app een melding die gericht is op deze inschrijving verzenden. Voor meer informatie over het toosend meldingen, Zie [Routering en code-expressies](notification-hubs-tags-segment-push-message.md).
Merk op dat in dit geval gebruikt u luistert alleen rechten tooaccess uw notification hubs van Hallo-apparaat. Zie voor meer informatie [beveiliging](notification-hubs-push-notification-security.md).

Registreren van apparaat Hallo Hallo eenvoudigste methode is, maar er enkele nadelen.
Hallo eerste nadeel is dat een client-app alleen de labels bijwerken kunt wanneer Hallo app actief is. Bijvoorbeeld, als een gebruiker heeft twee apparaten die geregistreerd labels gerelateerde toosport teams, wanneer de eerste apparaat Hallo zich voor een aanvullende code (bijvoorbeeld Seahawks registreert), Hallo tweede apparaat wordt niet Hallo meldingen ontvangen over Hallo Seahawks tot Hallo-app op Hallo tweede apparaat wordt een tweede keer worden uitgevoerd. Meer in het algemeen als labels worden beïnvloed door meerdere apparaten, is tags beheren vanuit Hallo back-end een wenselijk optie.
Hallo tweede nadeel van beheer van de registratie van de client-app Hallo is dat extra aandacht beveiligen Hallo registratie toospecific tags is vereist omdat apps kunnen worden hacked, zoals wordt beschreven in de sectie Hallo "Tag beveiligingsniveau."

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-an-installation"></a>Voorbeeld van code tooregister met een notification hub van een apparaat gebruikmaakt van een installatie
Op dit moment is dit wordt alleen ondersteund met Hallo [Notification Hubs REST-API](https://msdn.microsoft.com/library/mt621153.aspx).

U kunt ook Hallo PATCH methode met behulp van Hallo [JSON-Patch standaard](https://tools.ietf.org/html/rfc6902) voor het bijwerken van Hallo-installatie.

    class DeviceInstallation
    {
        public string installationId { get; set; }
        public string platform { get; set; }
        public string pushChannel { get; set; }
        public string[] tags { get; set; }
    }

    private async Task<HttpStatusCode> CreateOrUpdateInstallationAsync(DeviceInstallation deviceInstallation,
         string hubName, string listenConnectionString)
    {
        if (deviceInstallation.installationId == null)
            return HttpStatusCode.BadRequest;

        // Parse connection string (https://msdn.microsoft.com/library/azure/dn495627.aspx)
        ConnectionStringUtility connectionSaSUtil = new ConnectionStringUtility(listenConnectionString);
        string hubResource = "installations/" + deviceInstallation.installationId + "?";
        string apiVersion = "api-version=2015-04";

        // Determine hello targetUri that we will sign
        string uri = connectionSaSUtil.Endpoint + hubName + "/" + hubResource + apiVersion;

        //=== Generate SaS Security Token for Authorization header ===
        // See, https://msdn.microsoft.com/library/azure/dn495627.aspx
        string SasToken = connectionSaSUtil.getSaSToken(uri, 60);

        using (var httpClient = new HttpClient())
        {
            string json = JsonConvert.SerializeObject(deviceInstallation);

            httpClient.DefaultRequestHeaders.Add("Authorization", SasToken);

            var response = await httpClient.PutAsync(uri, new StringContent(json, System.Text.Encoding.UTF8, "application/json"));
            return response.StatusCode;
        }
    }

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    string installationId = null;
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a installation id in application data, create and store as application data.
    if (!settings.ContainsKey("__NHInstallationId"))
    {
        installationId = Guid.NewGuid().ToString();
        settings.Add("__NHInstallationId", installationId);
    }

    installationId = (string)settings["__NHInstallationId"];

    var deviceInstallation = new DeviceInstallation
    {
        installationId = installationId,
        platform = "wns",
        pushChannel = channel.Uri,
        //tags = tags.ToArray<string>()
    };

    var statusCode = await CreateOrUpdateInstallationAsync(deviceInstallation, 
                        "<HUBNAME>", "<SHARED LISTEN CONNECTION STRING>");

    if (statusCode != HttpStatusCode.Accepted)
    {
        var dialog = new MessageDialog(statusCode.ToString(), "Registration failed. Installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }
    else
    {
        var dialog = new MessageDialog("Registration successful using installation Id : " + installationId);
        dialog.Commands.Add(new UICommand("OK"));
        await dialog.ShowAsync();
    }



#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration"></a>Voorbeeld van code tooregister met een notification hub van een apparaat een registratie
Deze methoden maken of bijwerken van een registratie voor Hallo-apparaat waarop ze worden aangeroepen. Dit betekent dat gehele Hallo-registratie in volgorde tooupdate Hallo ingang of Hallo labels, moet overschrijven. Houd er rekening mee dat registraties tijdelijk is en zijn dus moet u altijd een betrouwbare archief met huidige Hallo-labels die een specifiek apparaat moet hebben.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // hello Device id from hello PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from hello client itself, then store this registration id in device
    // storage. Then when hello app starts, you can check if a registration id already exists or not before
    // creating.
    var settings = ApplicationData.Current.LocalSettings.Values;

    // If we have not stored a registration id in application data, store in application data.
    if (!settings.ContainsKey("__NHRegistrationId"))
    {
        // make sure there are no existing registrations for this push handle (used for iOS and Android)    
        string newRegistrationId = null;
        var registrations = await hub.GetRegistrationsByChannelAsync(pushChannel.Uri, 100);
        foreach (RegistrationDescription registration in registrations)
        {
            if (newRegistrationId == null)
            {
                newRegistrationId = registration.RegistrationId;
            }
            else
            {
                await hub.DeleteRegistrationAsync(registration);
            }
        }

        newRegistrationId = await hub.CreateRegistrationIdAsync();

        settings.Add("__NHRegistrationId", newRegistrationId);
    }

    string regId = (string)settings["__NHRegistrationId"];

    RegistrationDescription registration = new WindowsRegistrationDescription(pushChannel.Uri);
    registration.RegistrationId = regId;
    registration.Tags = new HashSet<string>(YourTags);

    try
    {
        await hub.CreateOrUpdateRegistrationAsync(registration);
    }
    catch (Microsoft.WindowsAzure.Messaging.RegistrationGoneException e)
    {
        settings.Remove("__NHRegistrationId");
    }


## <a name="registration-management-from-a-backend"></a>Beheer van de registratie van een back-end
Registraties vanuit Hallo back-end beheren, moet aanvullende code schrijven. Hallo-app vanaf Hallo apparaat moet bijgewerkte PNS-ingang toohello back-end Hallo telkens wanneer Hallo-app wordt gestart (samen met tags en sjablonen) en Hallo back-end moet bijwerken deze ingang op Hallo notification hub opgeven. Hallo volgende afbeelding ziet u dit ontwerp.

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

Hallo voordelen registraties vanuit Hallo back-end beheren Hallo mogelijkheid toomodify labels tooregistrations zelfs wanneer de bijbehorende app Hallo op Hallo-apparaat is niet actief en tooauthenticate Hallo client-app voordat u de registratie van een tag tooits toevoegt.

#### <a name="example-code-tooregister-with-a-notification-hub-from-a-backend-using-an-installation"></a>Voorbeeld van code tooregister met een notification hub vanuit een back-end gebruikmaakt van een installatie
Hallo-clientapparaat nog steeds de PNS-ingang en relevante installatie-eigenschappen als voorheen en aanroepen van aangepaste API op Hallo backend die kunt Hallo-registratie uitvoeren en autoriseren enzovoort Hallo back-end-tags kunnen gebruikmaken van Hallo [Notification Hub SDK voor back-end operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

U kunt ook Hallo PATCH methode met behulp van Hallo [JSON-Patch standaard](https://tools.ietf.org/html/rfc6902) voor het bijwerken van Hallo-installatie.

    // Initialize hello Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on hello backend
    public async Task<HttpResponseMessage> Put(DeviceInstallation deviceUpdate)
    {

        Installation installation = new Installation();
        installation.InstallationId = deviceUpdate.InstallationId;
        installation.PushChannel = deviceUpdate.Handle;
        installation.Tags = deviceUpdate.Tags;

        switch (deviceUpdate.Platform)
        {
            case "mpns":
                installation.Platform = NotificationPlatform.Mpns;
                break;
            case "wns":
                installation.Platform = NotificationPlatform.Wns;
                break;
            case "apns":
                installation.Platform = NotificationPlatform.Apns;
                break;
            case "gcm":
                installation.Platform = NotificationPlatform.Gcm;
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }


        // In hello backend we can control if a user is allowed tooadd tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-tooregister-with-a-notification-hub-from-a-device-using-a-registration-id"></a>Voorbeeld van code tooregister met een notification hub van een apparaat een registratie-id
U kunt CRUDS basisbewerkingen op registraties uitvoeren van uw app-end. Bijvoorbeeld:

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of hello correct type, e.g.
    var reg = new WindowsRegistrationDescription(channelUri, tags);

    // Create
    await hub.CreateRegistrationAsync(reg);

    // Get by id
    var r = await hub.GetRegistrationAsync<RegistrationDescription>("id");

    // update
    r.Tags.Add("myTag");

    // update on hub
    await hub.UpdateRegistrationAsync(r);

    // delete
    await hub.DeleteRegistrationAsync(r);


Hallo back-end moet verwerken gelijktijdigheid van taken tussen registratie-updates. Service Bus biedt Optimistisch gelijktijdigheidbeheer voor het beheer van de registratie. Dit is geïmplementeerd op Hallo HTTP-niveau met Hallo gebruik van ETag op beheerbewerkingen voor registratie. Deze functie is transparant gebruikt door de Microsoft-SDKs die Veroorzaak een exception als een update is geweigerd voor gelijktijdigheid redenen. Hallo app back-end is verantwoordelijk voor het verwerken van deze uitzonderingen en Hallo update opnieuw, indien nodig.


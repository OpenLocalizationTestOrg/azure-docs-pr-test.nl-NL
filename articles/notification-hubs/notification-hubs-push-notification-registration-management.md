---
title: Registratie van beheer
description: In dit onderwerp wordt uitgelegd hoe u apparaten registreren met notification hubs kunnen pushmeldingen worden ontvangen.
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
ms.openlocfilehash: a1a349150ef4c7837932706f0c4fcc8d022ec7ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="registration-management"></a><span data-ttu-id="4cd62-103">Registratiebeheer</span><span class="sxs-lookup"><span data-stu-id="4cd62-103">Registration management</span></span>
## <a name="overview"></a><span data-ttu-id="4cd62-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4cd62-104">Overview</span></span>
<span data-ttu-id="4cd62-105">In dit onderwerp wordt uitgelegd hoe u apparaten registreren met notification hubs kunnen pushmeldingen worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="4cd62-105">This topic explains how to register devices with notification hubs in order to receive push notifications.</span></span> <span data-ttu-id="4cd62-106">Het onderwerp wordt beschreven registraties op hoog niveau en vervolgens maakt u kennis met de twee belangrijkste patronen voor het registreren van apparaten: registreren van het apparaat rechtstreeks met de notification hub en registreren via een back-end voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="4cd62-106">The topic describes registrations at a high level, then introduces the two main patterns for registering devices: registering from the device directly to the notification hub, and registering through an application backend.</span></span> 

## <a name="what-is-device-registration"></a><span data-ttu-id="4cd62-107">Wat is de registratie</span><span class="sxs-lookup"><span data-stu-id="4cd62-107">What is device registration</span></span>
<span data-ttu-id="4cd62-108">Registreren van apparaten met een Notification Hub wordt bereikt met een **registratie** of **installatie**.</span><span class="sxs-lookup"><span data-stu-id="4cd62-108">Device registration with a Notification Hub is accomplished using a **Registration** or **Installation**.</span></span>

#### <a name="registrations"></a><span data-ttu-id="4cd62-109">Registraties</span><span class="sxs-lookup"><span data-stu-id="4cd62-109">Registrations</span></span>
<span data-ttu-id="4cd62-110">Een registratie koppelt de ingang Platform Notification Service (PNS) voor een apparaat met tags en mogelijk een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="4cd62-110">A registration associates the Platform Notification Service (PNS) handle for a device with tags and possibly a template.</span></span> <span data-ttu-id="4cd62-111">De PNS-ingang is mogelijk een ChannelURI, apparaattoken of GCM-registratie-id.</span><span class="sxs-lookup"><span data-stu-id="4cd62-111">The PNS handle could be a ChannelURI, device token, or GCM registration id.</span></span> <span data-ttu-id="4cd62-112">Labels worden gebruikt voor het routeren van meldingen naar de juiste set apparaat verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4cd62-112">Tags are used to route notifications to the correct set of device handles.</span></span> <span data-ttu-id="4cd62-113">Zie voor meer informatie [Routering en code-expressies](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="4cd62-113">For more information, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span> <span data-ttu-id="4cd62-114">Sjablonen worden gebruikt voor de per-registratie transformatie implementeren.</span><span class="sxs-lookup"><span data-stu-id="4cd62-114">Templates are used to implement per-registration transformation.</span></span> <span data-ttu-id="4cd62-115">Zie voor meer informatie [sjablonen](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="4cd62-115">For more information, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>

#### <a name="installations"></a><span data-ttu-id="4cd62-116">Installaties</span><span class="sxs-lookup"><span data-stu-id="4cd62-116">Installations</span></span>
<span data-ttu-id="4cd62-117">Een installatie is een uitgebreide registratie met een groot aantal push gerelateerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4cd62-117">An Installation is an enhanced registration that includes a bag of push related properties.</span></span> <span data-ttu-id="4cd62-118">Het is de nieuwste en beste aanpak voor het registreren van uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="4cd62-118">It is the latest and best approach to registering your devices.</span></span> <span data-ttu-id="4cd62-119">Echter niet ondersteund door de clientkant .NET SDK ([Notification Hub SDK voor back-end-bewerkingen](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) vanaf nog.</span><span class="sxs-lookup"><span data-stu-id="4cd62-119">However, it is not supported by client side .NET SDK ([Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/)) as of yet.</span></span>  <span data-ttu-id="4cd62-120">Dit betekent dat als u vanaf het clientapparaat zelf registreert, moet u zou gebruiken de [Notification Hubs REST-API](https://msdn.microsoft.com/library/mt621153.aspx) benadering voor ondersteuning van installaties.</span><span class="sxs-lookup"><span data-stu-id="4cd62-120">This means if you are registering from the client device itself, you would have to use the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx) approach to support installations.</span></span> <span data-ttu-id="4cd62-121">Als u een back-endservice gebruikt, moet u gebruikmaken van [Notification Hub SDK voor back-end-bewerkingen](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="4cd62-121">If you are using a backend service, you should be able to use [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="4cd62-122">Hier volgen enkele belangrijke voordelen voor het gebruik van installaties:</span><span class="sxs-lookup"><span data-stu-id="4cd62-122">The following are some key advantages to using installations:</span></span>

* <span data-ttu-id="4cd62-123">Maken of bijwerken van een installatie is volledig idempotent.</span><span class="sxs-lookup"><span data-stu-id="4cd62-123">Creating or updating an installation is fully idempotent.</span></span> <span data-ttu-id="4cd62-124">Zo kunt u het opnieuw zonder vragen over dubbele registraties.</span><span class="sxs-lookup"><span data-stu-id="4cd62-124">So you can retry it without any concerns about duplicate registrations.</span></span>
* <span data-ttu-id="4cd62-125">Het installatiemodel kunt eenvoudig doen afzonderlijke pushes - doelen specifiek apparaat.</span><span class="sxs-lookup"><span data-stu-id="4cd62-125">The installation model makes it easy to do individual pushes - targeting specific device.</span></span> <span data-ttu-id="4cd62-126">Een Systeemlabel **' $InstallationId: [omwille van] '** automatisch met elke installatie op basis van de registratie wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4cd62-126">A system tag **"$InstallationId:[installationId]"** is automatically added with each installation based registration.</span></span> <span data-ttu-id="4cd62-127">U kunt dus een verzenden naar deze code op een specifiek apparaat zonder extra programmeren aanroepen.</span><span class="sxs-lookup"><span data-stu-id="4cd62-127">So you can call a send to this tag to target a specific device without having to do any additional coding.</span></span>
* <span data-ttu-id="4cd62-128">Met installaties kunt u doen gedeeltelijke registratie-updates.</span><span class="sxs-lookup"><span data-stu-id="4cd62-128">Using installations also enables you to do partial registration updates.</span></span> <span data-ttu-id="4cd62-129">De gedeeltelijke update van een installatie wordt aangevraagd met een PATCH methode met de [JSON-Patch standaard](https://tools.ietf.org/html/rfc6902).</span><span class="sxs-lookup"><span data-stu-id="4cd62-129">The partial update of an installation is requested with a PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902).</span></span> <span data-ttu-id="4cd62-130">Dit is bijzonder nuttig wanneer u wilt bijwerken, tags voor de registratie.</span><span class="sxs-lookup"><span data-stu-id="4cd62-130">This is particularly useful when you want to update tags on the registration.</span></span> <span data-ttu-id="4cd62-131">U hoeft te halen de registratie van de gehele en verzend de vorige labels opnieuw.</span><span class="sxs-lookup"><span data-stu-id="4cd62-131">You don't have to pull down the entire registration and then resend all the previous tags again.</span></span>

<span data-ttu-id="4cd62-132">Een installatie mag de volgende eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4cd62-132">An installation can contain the the following properties.</span></span> <span data-ttu-id="4cd62-133">Voor een volledig overzicht van de installatie-eigenschappen-Zie [maken of een installatie met REST-API worden overschreven](https://msdn.microsoft.com/library/azure/mt621153.aspx) of [installatie-eigenschappen](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) voor de.</span><span class="sxs-lookup"><span data-stu-id="4cd62-133">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST API](https://msdn.microsoft.com/library/azure/mt621153.aspx) or [Installation Properties](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.installation_properties.aspx) for the .</span></span>

    // Example installation format to show some supported properties
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



<span data-ttu-id="4cd62-134">Het is belangrijk te weten dat registraties en installaties standaard niet langer verloopt.</span><span class="sxs-lookup"><span data-stu-id="4cd62-134">It is important to note that registrations and installations by default no longer expire.</span></span>

<span data-ttu-id="4cd62-135">Registraties en installaties moeten een geldige PNS-ingang voor elk apparaat/kanaal bevatten.</span><span class="sxs-lookup"><span data-stu-id="4cd62-135">Registrations and installations must contain a valid PNS handle for each device/channel.</span></span> <span data-ttu-id="4cd62-136">Omdat de PNS-ingangen kunnen alleen worden verkregen in een client-app op het apparaat, wordt een patroon is rechtstreeks op het apparaat aan de clientapp registreren.</span><span class="sxs-lookup"><span data-stu-id="4cd62-136">Because PNS handles can only be obtained in a client app on the device, one pattern is to register directly on that device with the client app.</span></span> <span data-ttu-id="4cd62-137">Aan de andere kant beveiligingsoverwegingen en zakelijke logica die zijn gerelateerd aan tags u mogelijk voor het beheren van de apparaatregistratie in de back-end van de app.</span><span class="sxs-lookup"><span data-stu-id="4cd62-137">On the other hand, security considerations and business logic related to tags might require you to manage device registration in the app back-end.</span></span> 

#### <a name="templates"></a><span data-ttu-id="4cd62-138">Sjablonen</span><span class="sxs-lookup"><span data-stu-id="4cd62-138">Templates</span></span>
<span data-ttu-id="4cd62-139">Als u wilt gebruiken [sjablonen](notification-hubs-templates-cross-platform-push-messages.md), installatie van het apparaat ook bevatten alle sjablonen die zijn gekoppeld aan het apparaat in een JSON formatteren (Zie het bovenstaande voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="4cd62-139">If you want to use [Templates](notification-hubs-templates-cross-platform-push-messages.md), the device installation also hold all templates associated with that device in a JSON format (see sample above).</span></span> <span data-ttu-id="4cd62-140">De sjabloonnamen helpen bij het doel van verschillende sjablonen voor hetzelfde apparaat.</span><span class="sxs-lookup"><span data-stu-id="4cd62-140">The template names help target different templates for the same device.</span></span>

<span data-ttu-id="4cd62-141">Houd er rekening mee dat de sjabloonnaam van elke wordt toegewezen aan een instantie van de sjabloon en een optionele set van labels.</span><span class="sxs-lookup"><span data-stu-id="4cd62-141">Note that each template name maps to a template body and an optional set of tags.</span></span> <span data-ttu-id="4cd62-142">Elk platform kunt bovendien aanvullende Sjablooneigenschappen hebben.</span><span class="sxs-lookup"><span data-stu-id="4cd62-142">Moreover, each platform can have additional template properties.</span></span> <span data-ttu-id="4cd62-143">Voor Windows Store (met WNS) en Windows Phone 8 (met behulp van MPNS), kan een extra set van headers deel uitmaken van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="4cd62-143">For Windows Store (using WNS) and Windows Phone 8 (using MPNS), an additional set of headers can be part of the template.</span></span> <span data-ttu-id="4cd62-144">In het geval van APNs, kunt u een eigenschap verloopdatum instellen moet een constante of een sjabloonexpressie.</span><span class="sxs-lookup"><span data-stu-id="4cd62-144">In the case of APNs, you can set an expiry property to either a constant or to a template expression.</span></span> <span data-ttu-id="4cd62-145">Voor een volledig overzicht van de installatie-eigenschappen-Zie [maken of een installatie met REST overschrijven](https://msdn.microsoft.com/library/azure/mt621153.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="4cd62-145">For a complete listing of the installation properties see, [Create or Overwrite an Installation with REST](https://msdn.microsoft.com/library/azure/mt621153.aspx) topic.</span></span>

#### <a name="secondary-tiles-for-windows-store-apps"></a><span data-ttu-id="4cd62-146">Secundaire tegels voor Windows Store-Apps</span><span class="sxs-lookup"><span data-stu-id="4cd62-146">Secondary Tiles for Windows Store Apps</span></span>
<span data-ttu-id="4cd62-147">Voor toepassingen voor Windows Store-client, verzenden van meldingen naar secundaire tegels is hetzelfde als ze worden verzonden naar de primaire alias.</span><span class="sxs-lookup"><span data-stu-id="4cd62-147">For Windows Store client applications, sending notifications to secondary tiles is the same as sending them to the primary one.</span></span> <span data-ttu-id="4cd62-148">Dit wordt ook ondersteund in installaties.</span><span class="sxs-lookup"><span data-stu-id="4cd62-148">This is also supported in installations.</span></span> <span data-ttu-id="4cd62-149">Houd er rekening mee dat secundaire tegels hebben een verschillende ChannelUri die de SDK op uw clientapp transparant verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4cd62-149">Note that secondary tiles have a different ChannelUri, which the SDK on your client app handles transparently.</span></span>

<span data-ttu-id="4cd62-150">Het woordenboek SecondaryTiles maakt gebruik van de dezelfde TileId die wordt gebruikt voor het object SecondaryTiles in uw Windows Store-app niet maken.</span><span class="sxs-lookup"><span data-stu-id="4cd62-150">The SecondaryTiles dictionary uses the same TileId that is used to create the SecondaryTiles object in your Windows Store app.</span></span>
<span data-ttu-id="4cd62-151">Net als bij de primaire ChannelUri kunt ChannelUris secundaire tegels op elk moment wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4cd62-151">As with the primary ChannelUri, ChannelUris of secondary tiles can change at any moment.</span></span> <span data-ttu-id="4cd62-152">Om de installaties behouden in de notification hub is bijgewerkt, moet het apparaat te vernieuwen met de huidige ChannelUris van de secundaire tegels.</span><span class="sxs-lookup"><span data-stu-id="4cd62-152">In order to keep the installations in the notification hub updated, the device must refresh them with the current ChannelUris of the secondary tiles.</span></span>

## <a name="registration-management-from-the-device"></a><span data-ttu-id="4cd62-153">Beheer van de registratie van het apparaat</span><span class="sxs-lookup"><span data-stu-id="4cd62-153">Registration management from the device</span></span>
<span data-ttu-id="4cd62-154">Bij het beheren van de registratie van de client-apps, is alleen de back-end die verantwoordelijk is voor het verzenden van meldingen.</span><span class="sxs-lookup"><span data-stu-id="4cd62-154">When managing device registration from client apps, the backend is only responsible for sending notifications.</span></span> <span data-ttu-id="4cd62-155">Client-apps PNS-ingangen up-to-date te houden en registreer labels.</span><span class="sxs-lookup"><span data-stu-id="4cd62-155">Client apps keep PNS handles up to date, and register tags.</span></span> <span data-ttu-id="4cd62-156">De volgende afbeelding ziet u dit patroon.</span><span class="sxs-lookup"><span data-stu-id="4cd62-156">The following picture illustrates this pattern.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-device.png)

<span data-ttu-id="4cd62-157">Het apparaat eerst de PNS-ingang opgehaald uit de PNS vervolgens rechtstreeks door de notification hub geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="4cd62-157">The device first retrieves the PNS handle from the PNS, then registers with the notification hub directly.</span></span> <span data-ttu-id="4cd62-158">Nadat de registratie geslaagd is, kan de back-end voor de app een melding die gericht is op deze inschrijving verzenden.</span><span class="sxs-lookup"><span data-stu-id="4cd62-158">After the registration is successful, the app backend can send a notification targeting that registration.</span></span> <span data-ttu-id="4cd62-159">Zie voor meer informatie over het verzenden van meldingen [Routering en code-expressies](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="4cd62-159">For more information about how to send notifications, see [Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>
<span data-ttu-id="4cd62-160">Merk op dat in dit geval gebruikt u luistert alleen rechten voor toegang tot uw notification hubs van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="4cd62-160">Note that in this case, you will use only Listen rights to access your notification hubs from the device.</span></span> <span data-ttu-id="4cd62-161">Zie voor meer informatie [beveiliging](notification-hubs-push-notification-security.md).</span><span class="sxs-lookup"><span data-stu-id="4cd62-161">For more information, see [Security](notification-hubs-push-notification-security.md).</span></span>

<span data-ttu-id="4cd62-162">Registreren van het apparaat is de eenvoudigste methode, maar er enkele nadelen.</span><span class="sxs-lookup"><span data-stu-id="4cd62-162">Registering from the device is the simplest method, but it has some drawbacks.</span></span>
<span data-ttu-id="4cd62-163">Het eerste nadeel is dat een client-app alleen de labels bijwerken kunt wanneer de app actief is.</span><span class="sxs-lookup"><span data-stu-id="4cd62-163">The first drawback is that a client app can only update its tags when the app is active.</span></span> <span data-ttu-id="4cd62-164">Bijvoorbeeld, als een gebruiker heeft twee apparaten die geregistreerd labels die gerelateerd zijn aan sport-teams, wanneer het eerste apparaat voor een aanvullende code (bijvoorbeeld Seahawks registreert), zal het tweede apparaat het geen meldingen ontvangen over de Seahawks totdat de app op het tweede apparaat is een tweede keer uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4cd62-164">For example, if a user has two devices that register tags related to sport teams, when the first device registers for an additional tag (for example, Seahawks), the second device will not receive the notifications about the Seahawks until the app on the second device is executed a second time.</span></span> <span data-ttu-id="4cd62-165">Meer in het algemeen als labels worden beïnvloed door meerdere apparaten, is het beheren van de labels van de back-end een wenselijk optie.</span><span class="sxs-lookup"><span data-stu-id="4cd62-165">More generally, when tags are affected by multiple devices, managing tags from the backend is a desirable option.</span></span>
<span data-ttu-id="4cd62-166">Het tweede nadeel van beheer van de registratie van de client-app is dat extra aandacht beveiligen van de registratie aan specifieke tags is vereist omdat apps kunnen worden hacked, zoals wordt beschreven in de sectie "Tag beveiligingsniveau."</span><span class="sxs-lookup"><span data-stu-id="4cd62-166">The second drawback of registration management from the client app is that, since apps can be hacked, securing the registration to specific tags requires extra care, as explained in the section “Tag-level security.”</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-an-installation"></a><span data-ttu-id="4cd62-167">Voorbeeldcode registreren bij een notification hub van een apparaat gebruikmaakt van een installatie</span><span class="sxs-lookup"><span data-stu-id="4cd62-167">Example code to register with a notification hub from a device using an installation</span></span>
<span data-ttu-id="4cd62-168">Op dit moment is dit wordt alleen ondersteund met behulp van de [Notification Hubs REST-API](https://msdn.microsoft.com/library/mt621153.aspx).</span><span class="sxs-lookup"><span data-stu-id="4cd62-168">At this time, this is only supported using the [Notification Hubs REST API](https://msdn.microsoft.com/library/mt621153.aspx).</span></span>

<span data-ttu-id="4cd62-169">U kunt ook de PATCH methode met behulp van de [JSON-Patch standaard](https://tools.ietf.org/html/rfc6902) voor het bijwerken van de installatie.</span><span class="sxs-lookup"><span data-stu-id="4cd62-169">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

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

        // Determine the targetUri that we will sign
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



#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration"></a><span data-ttu-id="4cd62-170">Voorbeeldcode registreren bij een notification hub van een apparaat een registratie</span><span class="sxs-lookup"><span data-stu-id="4cd62-170">Example code to register with a notification hub from a device using a registration</span></span>
<span data-ttu-id="4cd62-171">Deze methoden maken of bijwerken van een registratie voor het apparaat waarop ze worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="4cd62-171">These methods create or update a registration for the device on which they are called.</span></span> <span data-ttu-id="4cd62-172">Dit betekent dat de registratie van de hele om bij te werken op de greep of de labels, moet overschrijven.</span><span class="sxs-lookup"><span data-stu-id="4cd62-172">This means that in order to update the handle or the tags, you must overwrite the entire registration.</span></span> <span data-ttu-id="4cd62-173">Houd er rekening mee dat registraties tijdelijk is en zijn dus moet u altijd een betrouwbare archief met de huidige codes die een specifiek apparaat moet hebben.</span><span class="sxs-lookup"><span data-stu-id="4cd62-173">Remember that registrations are transient, so you should always have a reliable store with the current tags that a specific device needs.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // The Device id from the PNS
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    // If you are registering from the client itself, then store this registration id in device
    // storage. Then when the app starts, you can check if a registration id already exists or not before
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


## <a name="registration-management-from-a-backend"></a><span data-ttu-id="4cd62-174">Beheer van de registratie van een back-end</span><span class="sxs-lookup"><span data-stu-id="4cd62-174">Registration management from a backend</span></span>
<span data-ttu-id="4cd62-175">Het beheer van registraties vanuit de back-end vereist aanvullende code schrijven.</span><span class="sxs-lookup"><span data-stu-id="4cd62-175">Managing registrations from the backend requires writing additional code.</span></span> <span data-ttu-id="4cd62-176">De app van het apparaat moet de bijgewerkte PNS-ingang naar de back-end telkens wanneer de app gestart (samen met tags en sjablonen) en de back-end moet bijwerken deze ingang op de notification hub opgeven.</span><span class="sxs-lookup"><span data-stu-id="4cd62-176">The app from the device must provide the updated PNS handle to the backend every time the app starts (along with tags and templates), and the backend must update this handle on the notification hub.</span></span> <span data-ttu-id="4cd62-177">De volgende afbeelding ziet u dit ontwerp.</span><span class="sxs-lookup"><span data-stu-id="4cd62-177">The following picture illustrates this design.</span></span>

![](./media/notification-hubs-registration-management/notification-hubs-registering-on-backend.png)

<span data-ttu-id="4cd62-178">De voordelen van het beheer van registraties vanuit de back-end zijn de mogelijkheid om te wijzigen van tags op registraties, zelfs wanneer de bijbehorende app op het apparaat is niet actief en de clientapp verifiëren voordat u een label toevoegt aan de registratie ervan.</span><span class="sxs-lookup"><span data-stu-id="4cd62-178">The advantages of managing registrations from the backend include the ability to modify tags to registrations even when the corresponding app on the device is inactive, and to authenticate the client app before adding a tag to its registration.</span></span>

#### <a name="example-code-to-register-with-a-notification-hub-from-a-backend-using-an-installation"></a><span data-ttu-id="4cd62-179">Voorbeeldcode registreren bij een notification hub vanuit een back-end gebruikmaakt van een installatie</span><span class="sxs-lookup"><span data-stu-id="4cd62-179">Example code to register with a notification hub from a backend using an installation</span></span>
<span data-ttu-id="4cd62-180">Het clientapparaat wordt nog steeds opgehaald van de PNS-ingang en relevante installatie-eigenschappen als voordat en aangepaste API aanroepen op de back-end die u kunt uitvoeren van de registratie en autoriseren van tags enzovoort. De back-end kunt gebruikmaken van de [Notification Hub SDK voor back-end-bewerkingen](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="4cd62-180">The client device still gets its PNS handle and relevant installation properties as before and calls a custom API on the backend that can perform the registration and authorize tags etc. The backend can leverage the [Notification Hub SDK for backend operations](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="4cd62-181">U kunt ook de PATCH methode met behulp van de [JSON-Patch standaard](https://tools.ietf.org/html/rfc6902) voor het bijwerken van de installatie.</span><span class="sxs-lookup"><span data-stu-id="4cd62-181">You can also use the PATCH method using the [JSON-Patch standard](https://tools.ietf.org/html/rfc6902) for updating the installation.</span></span>

    // Initialize the Notification Hub
    NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString(listenConnString, hubName);

    // Custom API on the backend
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


        // In the backend we can control if a user is allowed to add tags
        //installation.Tags = new List<string>(deviceUpdate.Tags);
        //installation.Tags.Add("username:" + username);

        await hub.CreateOrUpdateInstallationAsync(installation);

        return Request.CreateResponse(HttpStatusCode.OK);
    }


#### <a name="example-code-to-register-with-a-notification-hub-from-a-device-using-a-registration-id"></a><span data-ttu-id="4cd62-182">Voorbeeldcode registreren bij een notification hub van een apparaat een registratie-id</span><span class="sxs-lookup"><span data-stu-id="4cd62-182">Example code to register with a notification hub from a device using a registration id</span></span>
<span data-ttu-id="4cd62-183">U kunt CRUDS basisbewerkingen op registraties uitvoeren van uw app-end.</span><span class="sxs-lookup"><span data-stu-id="4cd62-183">From your app backend, you can perform basic CRUDS operations on registrations.</span></span> <span data-ttu-id="4cd62-184">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4cd62-184">For example:</span></span>

    var hub = NotificationHubClient.CreateClientFromConnectionString("{connectionString}", "hubName");

    // create a registration description object of the correct type, e.g.
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


<span data-ttu-id="4cd62-185">De back-end moet verwerken gelijktijdigheid van taken tussen registratie-updates.</span><span class="sxs-lookup"><span data-stu-id="4cd62-185">The backend must handle concurrency between registration updates.</span></span> <span data-ttu-id="4cd62-186">Service Bus biedt Optimistisch gelijktijdigheidbeheer voor het beheer van de registratie.</span><span class="sxs-lookup"><span data-stu-id="4cd62-186">Service Bus offers optimistic concurrency control for registration management.</span></span> <span data-ttu-id="4cd62-187">Dit is met het gebruik van ETag op beheerbewerkingen registratie geïmplementeerd op het niveau van HTTP.</span><span class="sxs-lookup"><span data-stu-id="4cd62-187">At the HTTP level, this is implemented with the use of ETag on registration management operations.</span></span> <span data-ttu-id="4cd62-188">Deze functie is transparant gebruikt door de Microsoft-SDKs die Veroorzaak een exception als een update is geweigerd voor gelijktijdigheid redenen.</span><span class="sxs-lookup"><span data-stu-id="4cd62-188">This feature is transparently used by Microsoft SDKs, which throw an exception if an update is rejected for concurrency reasons.</span></span> <span data-ttu-id="4cd62-189">De app-back-end is verantwoordelijk voor het verwerken van deze uitzonderingen en de update opnieuw, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="4cd62-189">The app backend is responsible for handling these exceptions and retrying the update if required.</span></span>

